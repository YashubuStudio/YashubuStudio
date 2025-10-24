# Open JTalkレポート

これは実際にRaspberryPi 4B（4GB）でOpen JTalkを実行した際のレポートです。

## Open JTalk

入力された日本語テキストに基づいて自由な音声を生成するHMMテキスト音声合成システム，Open JTalkのデモンストレーションです．
https://open-jtalk.sp.nitech.ac.jp/

## ざっくりメモリ使用量

- 初期化（warmup）で +12.7MB、以降の常用ワーキングセットは 約 50–70MB

- 短文は ΔRSS ~+1MB、中くらいで ~+10MB

- 長文（約16.5s）は一時ピーク ~212MB（終了後は 66MB に収束）
→ 波形を丸ごと保持するため、長尺・高サンプルレートほどピークが跳る

なお、CPUはそれほど跳ねず

## 必要なパッケージ

### system (apt)

RaspberryPi OS （2025/10/24）

- build-essential

### venv (pip)

- numpy
- pyopenjtalk

## 最小コード

```
# ~/Desktop/smoke_pyopenjtalk_fix.py
import os, wave
import numpy as np
import pyopenjtalk

def to_pcm16_auto(x: np.ndarray) -> np.ndarray:
    """pyopenjtalk出力の実スケールを自動判定して int16(LE) に変換"""
    if x.dtype == np.int16:
        pcm = x
    else:
        x = np.asarray(x, dtype=np.float64)
        amax = float(np.max(np.abs(x))) if x.size else 0.0

        if amax == 0.0:
            pcm = np.zeros_like(x, dtype=np.int16)
        elif amax <= 1.5:
            # 正規化float [-1,1] 想定
            pcm = np.clip(x, -1.0, 1.0)
            pcm = (pcm * 32767.0).astype(np.int16, copy=False)
        elif amax <= 40000.0:
            # すでにint16スケールなfloat（±32767周辺）
            pcm = np.clip(x, -32768.0, 32767.0).astype(np.int16, copy=False)
        else:
            # 予期せぬスケール → 正規化してからint16化
            pcm = (x / amax)
            pcm = np.clip(pcm, -1.0, 1.0)
            pcm = (pcm * 32767.0).astype(np.int16, copy=False)

    # little-endian & C連続化
    return np.ascontiguousarray(pcm.astype('<i2', copy=False))

def write_wav_le16(path: str, pcm16: np.ndarray, sr: int):
    with wave.open(path, 'wb') as wf:
        wf.setnchannels(1)
        wf.setsampwidth(2)
        wf.setframerate(sr)
        wf.writeframes(pcm16.tobytes())

def stats(tag, x_i16):
    x = x_i16.astype(np.float64)
    rms = np.sqrt(np.mean(x**2))
    clip = (np.sum(x == 32767) + np.sum(x == -32768)) / x.size
    print(f"[{tag}] min={x.min():.0f} max={x.max():.0f} rms={rms:.1f} clip={clip*100:.3f}%")

def main():
    text = "こんにちは。Open JTalk を Python だけで使っています。これはスケール修正後のテストです。"
    wav, sr = pyopenjtalk.tts(text)

    # 変換前の実スケールを参考表示
    amax = float(np.max(np.abs(wav))) if wav.size else 0.0
    print("pyopenjtalk dtype:", wav.dtype, "amax:", amax)

    pcm16 = to_pcm16_auto(wav)
    stats("converted", pcm16)

    out = os.path.expanduser("~/Desktop/hello_pyjtalk_fixed.wav")
    write_wav_le16(out, pcm16, sr)
    print("Saved:", out, "(sr=", sr, ")")

if __name__ == "__main__":
    main()
```

## メモリ使用量確認の実データ

### RAM

```
=== pyopenjtalk RSS measurement (Python-only) ===
Start RSS: 37.7 MB  | ru_maxrss: 37.7 MB

[warmup] time=0.671s  sr=48000Hz
  RSS before: 37.7 MB  after: 50.4 MB  Δ: +12.7 MB
  Peak RSS during: 50.2 MB  (Δ vs before: +12.4 MB)
  ru_maxrss (proc lifetime): before 37.7 MB -> after 51.8 MB  (Δ +14.1 MB)
  saved: /home/ysu/Desktop/warmup.wav

[short] time=0.588s  sr=48000Hz
  RSS before: 50.4 MB  after: 51.5 MB  Δ: +1.1 MB
  Peak RSS during: 54.4 MB  (Δ vs before: +4.0 MB)
  ru_maxrss (proc lifetime): before 51.8 MB -> after 54.3 MB  (Δ +2.6 MB)
  saved: /home/ysu/Desktop/short.wav

[mid] time=1.175s  sr=48000Hz
  RSS before: 51.5 MB  after: 61.5 MB  Δ: +10.0 MB
  Peak RSS during: 64.2 MB  (Δ vs before: +12.7 MB)
  ru_maxrss (proc lifetime): before 54.3 MB -> after 64.1 MB  (Δ +9.7 MB)
  saved: /home/ysu/Desktop/mid.wav

[long] time=16.490s  sr=48000Hz
  RSS before: 61.5 MB  after: 139.9 MB  Δ: +78.4 MB
  Peak RSS during: 212.4 MB  (Δ vs before: +150.9 MB)
  ru_maxrss (proc lifetime): before 64.1 MB -> after 212.3 MB  (Δ +148.2 MB)
  saved: /home/ysu/Desktop/long.wav

[burst_00] time=0.754s  sr=48000Hz
  RSS before: 139.9 MB  after: 140.8 MB  Δ: +0.9 MB
  Peak RSS during: 140.8 MB  (Δ vs before: +0.9 MB)
  ru_maxrss (proc lifetime): before 212.3 MB -> after 212.3 MB  (Δ +0.0 MB)
  saved: /home/ysu/Desktop/burst_00.wav

[burst_01] time=0.778s  sr=48000Hz
  RSS before: 140.8 MB  after: 66.4 MB  Δ: -74.5 MB
  Peak RSS during: 140.8 MB  (Δ vs before: +0.0 MB)
  ru_maxrss (proc lifetime): before 212.3 MB -> after 212.3 MB  (Δ +0.0 MB)
  saved: /home/ysu/Desktop/burst_01.wav

[burst_02] time=0.735s  sr=48000Hz
  RSS before: 66.4 MB  after: 66.4 MB  Δ: +0.0 MB
  Peak RSS during: 66.4 MB  (Δ vs before: +0.0 MB)
  ru_maxrss (proc lifetime): before 212.3 MB -> after 212.3 MB  (Δ +0.0 MB)
  saved: /home/ysu/Desktop/burst_02.wav

[burst_03] time=0.749s  sr=48000Hz
  RSS before: 66.4 MB  after: 66.4 MB  Δ: +0.0 MB
  Peak RSS during: 66.4 MB  (Δ vs before: +0.0 MB)
  ru_maxrss (proc lifetime): before 212.3 MB -> after 212.3 MB  (Δ +0.0 MB)
  saved: /home/ysu/Desktop/burst_03.wav

[burst_04] time=0.739s  sr=48000Hz
  RSS before: 66.4 MB  after: 66.4 MB  Δ: +0.0 MB
  Peak RSS during: 66.4 MB  (Δ vs before: +0.0 MB)
  ru_maxrss (proc lifetime): before 212.3 MB -> after 212.3 MB  (Δ +0.0 MB)
  saved: /home/ysu/Desktop/burst_04.wav

End RSS: 66.4 MB  | ru_maxrss (final): 212.3 MB 
```

### RAM Check Code

```
# ~/Desktop/measure_pyopenjtalk_rss.py
import os, time, wave, threading
import numpy as np
import psutil
import pyopenjtalk
import resource  # Linux系で ru_maxrss が取れる

PROC = psutil.Process(os.getpid())

def rss_mb() -> float:
    return PROC.memory_info().rss / (1024*1024)

def ru_maxrss_mb() -> float:
    # Linux: KB単位で返ってくる
    return resource.getrusage(resource.RUSAGE_SELF).ru_maxrss / 1024.0

class PeakSampler:
    """実行中のピークRSSをポーリングで取得（軽量）"""
    def __init__(self, interval_sec: float = 0.02):
        self.interval = interval_sec
        self._peak = rss_mb()
        self._stop = threading.Event()
        self._th = threading.Thread(target=self._run, daemon=True)

    def _run(self):
        while not self._stop.is_set():
            v = rss_mb()
            if v > self._peak:
                self._peak = v
            time.sleep(self.interval)

    def start(self):
        self._peak = rss_mb()
        self._stop.clear()
        self._th.start()

    def stop(self):
        self._stop.set()
        self._th.join()

    @property
    def peak(self) -> float:
        return self._peak

# ===== WAV 保存は常に LE int16 で =====
def to_pcm16_auto(x: np.ndarray) -> np.ndarray:
    """pyopenjtalk出力の実スケールを自動判定して int16(LE) に変換"""
    if x.dtype == np.int16:
        pcm = x
    else:
        x = np.asarray(x, dtype=np.float64)
        amax = float(np.max(np.abs(x))) if x.size else 0.0
        if amax == 0.0:
            pcm = np.zeros_like(x, dtype=np.int16)
        elif amax <= 1.5:
            pcm = np.clip(x, -1.0, 1.0); pcm = (pcm * 32767.0).astype(np.int16, copy=False)
        elif amax <= 40000.0:
            pcm = np.clip(x, -32768.0, 32767.0).astype(np.int16, copy=False)
        else:
            pcm = (x / amax); pcm = np.clip(pcm, -1.0, 1.0); pcm = (pcm * 32767.0).astype(np.int16, copy=False)
    return np.ascontiguousarray(pcm.astype('<i2', copy=False))

def write_wav_le16(path: str, pcm16: np.ndarray, sr: int):
    with wave.open(path, 'wb') as wf:
        wf.setnchannels(1); wf.setsampwidth(2); wf.setframerate(sr)
        wf.writeframes(pcm16.tobytes())

def synth_to_wav(text: str, path: str):
    wav, sr = pyopenjtalk.tts(text)     # 完全ローカル合成
    pcm16 = to_pcm16_auto(wav)
    write_wav_le16(path, pcm16, sr)
    return sr

def measure_one(label: str, text: str, outdir: str = "~/Desktop"):
    outdir = os.path.expanduser(outdir)
    os.makedirs(outdir, exist_ok=True)
    out_wav = os.path.join(outdir, f"{label}.wav")

    rss_before = rss_mb()
    ru_before  = ru_maxrss_mb()
    sampler = PeakSampler(interval_sec=0.02)
    sampler.start()
    t0 = time.time()
    sr = synth_to_wav(text, out_wav)
    t1 = time.time()
    sampler.stop()
    rss_after = rss_mb()
    ru_after  = ru_maxrss_mb()

    print(f"[{label}] time={t1-t0:.3f}s  sr={sr}Hz")
    print(f"  RSS before: {rss_before:.1f} MB  after: {rss_after:.1f} MB  Δ: {rss_after-rss_before:+.1f} MB")
    print(f"  Peak RSS during: {sampler.peak:.1f} MB  (Δ vs before: {sampler.peak-rss_before:+.1f} MB)")
    print(f"  ru_maxrss (proc lifetime): before {ru_before:.1f} MB -> after {ru_after:.1f} MB  (Δ {ru_after-ru_before:+.1f} MB)")
    print(f"  saved: {out_wav}\n")

def main():
    print("=== pyopenjtalk RSS measurement (Python-only) ===")
    print(f"Start RSS: {rss_mb():.1f} MB  | ru_maxrss: {ru_maxrss_mb():.1f} MB\n")

    # 初回ロードのコストを分離（ウォームアップ）
    measure_one("warmup", "ウォームアップです。これは最初の読み込みを含みます。")

    # 実測ケース
    short = "こんにちは。メモリ使用量を計測しています。"
    mid   = "Open JTalk は完全ローカルで動作し、辞書と音声モデルがあればオフラインで読み上げできます。"
    long  = "長文テストです。" + "日本語の文章を長く読み上げたときのメモリ使用量を確認します。" * 20

    measure_one("short", short)
    measure_one("mid",   mid)
    measure_one("long",  long)

    # バースト（連続合成）
    for i in range(5):
        measure_one(f"burst_{i:02}", f"連続合成の計測です。番号は {i} です。")

    print(f"End RSS: {rss_mb():.1f} MB  | ru_maxrss (final): {ru_maxrss_mb():.1f} MB")

if __name__ == "__main__":
    main()
```