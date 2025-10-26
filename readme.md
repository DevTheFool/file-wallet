# File-Wallet: Cryptocurrency Wallet Generator

![showcase.gif](https://github.com/DevTheFool/file-wallet/assets/110111354/a90eede3-f111-460c-86af-dbe9fbbbb385)

Official url: https://file-wallet.com/

This website allows you to generate valid cryptocurrency wallets completely offline, client side, using an image (or any other file) combined with an optional password, rather than the traditional random number generator.

## Why Use It?

There are several advantages in using a file and a password:

- **Hidden in Plain Sight:** Your file can be any ordinary image or document that can be stored on any device, disguising its critical role in the wallet creation.
- **Versatility Against Threats:** By changing the password, one file can be the source of multiple wallets. It's virtually impossible to determine how many wallets, if any, originated from a single file. This obscures potential theft attempts, including the so-called "$5 wrench attack".
- **Memorability:** It's easier to recall an image and a chosen password than to remember a randomized 24-word seed.

## How Does It Work?
It works fully offline, on the client:
1. The chosen file is transformed into a data URL (a string representation).
2. If a password is added, it's attached to the end of this string.
3. The concatenated string is hashed using SHA-256, which then becomes the entropy for the wallet generation. The wallet generation code is sourced from [iancoleman's bip39](https://github.com/iancoleman/bip39) and [bip39-coinomi](https://github.com/Coinomi/bip39-coinomi) for Monero.

```javascript
// All generated addresses are made with BIP44:
// `m/44'/Coin'/0'/0/Index`

Entropy = sha256(FileAsDataURL + Password);
MnemonicSeed = getMnemonicFromEntropy(Entropy);
```

## Safety Measures

- **File Integrity:** Ensure the file hasn't been compressed after you've used it to generate a wallet. It must remain unchanged, byte-for-byte. This is especially crucial for images; popular messaging apps tend to compress them, which would make them completely different to the wallet generator.
- **Password Selection:** It's crucial to use a password. Phrases, long but memorable, are recommended. For example: "My 3.14 dog thinks about 42 :)." Relating the phrase to the image can aid recall, but adding at least one random number and a special character is a must.
- **Device Trustworthiness:** Only use this website on devices you trust and preferably offline.
- **QR Code Precaution:** If you use the QR Code, you need to be careful, some scanner devices may store the scan history.

## How to Run It Offline?

Just disconnect the internet once the website is loaded :p

Or better, download the stand-alone "file-wallet.html" from the latest [releases](https://github.com/DevTheFool/file-wallet/releases), and open it with any browser (double click it).

I strongly recommend storing and using the "file-wallet.html" offline, to always have a copy of the website with the exact version you used, in the unlikely case the website is taken down in the future or the domain is taken over or the wallet generation algorithm changed.
