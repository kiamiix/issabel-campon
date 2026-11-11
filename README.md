# issabel-campon

Camp-on ("ring me back when free") for Issabel PBX (chan_sip). No module to install: one block of `extensions_custom.conf`.

قابلیت «خبرم کن وقتی آزاد شد» برای ایزابل (chan_sip)، بدون نصب ماژول: فقط یک تکه دایال‌پلن.

به داخلی‌ای زنگ می‌زنید که مشغول است. پیام پخش می‌شود: با **۱** تماس قطع می‌شود و هر وقت هر دو گوشی آزاد شدند (حداکثر ۳۰ دقیقه) گوشی شما زنگ می‌خورد و با برداشتن، داخلی مقصد گرفته می‌شود. بدون زدن ۱ تماس مثل قبل پشت‌خطی می‌شود

## What it does

An extension calls another extension that is on a call. A prompt plays: press **1**, the call ends, and the server rings you back as soon as both phones are free (max 30 min), then dials the other extension when you pick up. Without **1** the call continues as a normal call-waiting call.
.

## Install

Written on an Issabel server running Asterisk 18 with chan_sip. Back up `/etc/asterisk/extensions_custom.conf` first.

1. Append `extensions_custom.conf` from this repo to `/etc/asterisk/extensions_custom.conf`. In `[from-internal-custom]`, list your own extensions (one line each).
2. Upload a recording named `campon-prompt` in **PBX → System Recordings** (wav, 8 kHz, mono). The feature stays off until this file exists.
3. Run `asterisk -rx "dialplan reload"`.

To undo, remove the block and reload.

## Limits

- chan_sip only (`SIP/` channels, device name equal to extension number). Not written for PJSIP.
- Only direct extension-to-extension calls; ring groups, queues, and trunk calls are untouched.
- The extension list is static.
- Pressing 1 several times queues several requests.
- If you do not pick up the ring-back within 25 s, the request is dropped.

## See also

[issabel-missed-call-callback](https://github.com/kiamiix/issabel-missed-call-callback): route a returning caller to the extension that called them.

## License

MIT
