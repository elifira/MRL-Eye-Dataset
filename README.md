# CNN ile Göz Hastalığı Sınıflandırması


Bu proje, MRL Eye Dataset kullanarak CNN (Convolutional Neural Network) ile göz hastalıklarını sınıflandırmayı amaçlamaktadır. 

## Proje Hakkında

MRL Eye Dataset'inde bulunan göz görüntülerini "awake" (uyanık) ve "sleepy" (uykulu) olmak üzere iki sınıfa ayıran bir binary classification modeli geliştirdim. Toplam 84,898 görüntü ile çalıştım.

**Veri Seti Dağılımı:**
- Train: 50,937 görüntü
- Validation: 16,980 görüntü  
- Test: 16,981 görüntü


## Kullanılan Yöntemler
- **CNN Mimarisi**: Sıfırdan bir Convolutional Neural Network oluşturdum
- **Data Augmentation**: Rotation, zoom ve horizontal flip teknikleri kullandım
- **Hiperparametre Optimizasyonu**: 7 farklı konfigürasyon test ettim
- **Grad-CAM**: Modelin hangi bölgelere odaklandığını görselleştirdim


## Elde Edilen Sonuçlar

Model eğitimi sırasında bazı teknik sorunlar yaşadım ve eğitim tamamlanamadı. Ancak ilk epoch'ta %94.94 validation accuracy elde ettim. Test setinde %53.15 accuracy ile sınıflandırma yapabildim.

**Önemli Bulgular:**
- Model "awake" sınıfını daha sık tahmin ediyor
- "Sleepy" sınıfı için yüksek precision (0.95) ama düşük recall (0.05) var
- Sınıf dengesizliği problemi mevcut
- Model aslında "awake" sınıfını neredeyse her zaman tahmin ediyor (recall: 1.00). Bu da demek oluyor ki model çok konservatif davranıyor ve "sleepy" sınıfını neredeyse hiç tahmin etmiyor.

*Neden böyle oldu:**
1. **Sınıf dengesizliği**: Veri setinde "awake" sınıfı daha fazla olabilir
2. **Model eğitimi yetersiz**: Sadece 1 epoch eğitim yapabildim
3. **Threshold problemi**: 0.5 threshold'u optimal olmayabilir


- Gerçek hayatta kullanılabilmesi için model performansının artırılması şart

**Teknik Detaylar
   
### Hiperparametre Optimizasyonu
7 farklı konfigürasyon test ettim:
- Baseline model
- Daha fazla filtre (64, 128, 256)
- Yüksek dropout (0.5)
- L2 regularization (0.001)
- Büyük dense layer (256)
- Düşük learning rate (0.0001)
- RMSprop optimizer


**Detaylı Metrikler:**
- Test Accuracy: 53.15%
- Precision (Awake): 0.52
- Recall (Awake): 1.00
- F1-Score (Awake): 0.68
- Precision (Sleepy): 0.95
- Recall (Sleepy): 0.05
- F1-Score (Sleepy): 0.10


## Teknik Detaylar

- **Framework**: TensorFlow/Keras
- **Model Boyutu**: ~49.36 MB
- **Batch Size**: 32
- **Epochs**: 25 (early stopping ile)
- **Loss Function**: Binary Crossentropy
- **Callbacks**: EarlyStopping, ModelCheckpoint


## Sonuç ve Gelecek Çalışmalar

Bu projede CNN temellerini öğrendim, hiperparametre optimizasyonu deneyimi kazandım ve model yorumlama tekniklerini uyguladım. 

**Gelecek İyileştirmeler:**
- Transfer learning (VGG16, ResNet, EfficientNet) denemek
- Daha gelişmiş data augmentation (Mixup, CutMix)
- Sınıf dengesizliği için SMOTE veya class weighting
- Ensemble methods ile performans artırma
- Cross-validation ile daha güvenilir değerlendirme

**Kariyer Hedeflerim:**
- Psikoloji ve cognitive science alanında uzmanlaşma
- İnsan davranışı analizi ve yapay zeka entegrasyonu
- Nöropsikoloji ve beyin-bilgisayar arayüzleri

**Bu Projenin Gelecekteki Potansiyeli:**
- **Otomotiv sektörü**: Sürücü yorgunluk tespiti ve güvenlik sistemleri
- **Sağlık alanı**: Uyku bozuklukları ve nörolojik durumların tespiti
- **Psikoloji araştırmaları**: Dikkat, yorgunluk ve bilişsel yük analizi

  
**Teknik Geliştirmeler:**
- Transfer learning ile model performansını artırma
- Gerçek zamanlı video analizi için optimizasyon
- Web arayüzü ile kullanıcı dostu demo

## Kaggle Notebook
(https://www.kaggle.com/code/elifia/akbank/edit/run/264008185)

MRL Eye Dataset: https://www.kaggle.com/code/kimkijun7/mrl-eye-dataset-tf-cnn-with-python

