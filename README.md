# Başarı Can — varlıklar

Uygulamanın çalışma zamanında indirdiği dosyalar. Kaynak kod ayrı ve özel bir
depoda; burada yalnızca dağıtılan ikili dosyalar var.

Depo **herkese açık** olmak zorunda: özel bir depodan indirmek jeton ister,
jeton da uygulamanın içinde taşınırdı ve APK'dan çıkarılabilirdi. Model
gizli bir şey değil, jetonu sızdırmak ise gerçek bir güvenlik açığı.

## Sürümler

### `model-v1` — hece tanıma modeli

| Dosya | Boyut |
|---|---|
| `hece_ctc.int8.onnx` | 355.218.300 bayt |
| `hece_ctc_vocab.json` | 468 bayt |

Karakter düzeyi Türkçe CTC modeli (wav2vec2 türevi, dinamik int8).
Nicemleme `MatMulInteger` tabanlı — `ConvInteger` kullanan derleme cihazdaki
çalışma zamanında yürütülemiyor, o yüzden bu ayrım önemli.

Uygulama dosyaları ilk çalıştırmada indirir; sonrasında internet gerekmez.
Adresler derleme sırasında veriliyor:

```
flutter build apk --release --split-per-abi \
  --dart-define=CTC_MODEL_URL=https://github.com/drozkan22/basari-can-varliklar/releases/download/model-v1/hece_ctc.int8.onnx \
  --dart-define=CTC_VOCAB_URL=https://github.com/drozkan22/basari-can-varliklar/releases/download/model-v1/hece_ctc_vocab.json
```
