# Emlak İlanları Benzerlik Filteri

Bu proje, satılık emlak ilan açıklamalarını karşılaştırarak **yinelenen** ilanların tespit edilmesini amaçlamaktadır. Kullanıcılar, birden fazla ilan açıklamasının benzerliğini inceleyebilir ve veri temizliği işlemlerini kolaylaştırabilir. Proje, metin madenciliği ve doğal dil işleme tekniklerine dayanmaktadır. TF-IDF ve Word2Vec yöntemleri ile ilan açıklamaları arasındaki **metinsel benzerlik** ölçülmektedir.

---

## Modelin nasıl oluşturulacağı
1.**Veri Hazırlığı** 

-Google üzerinden Web Scraper eklentisi yardımıyla emlakjet.com ve hepsiemlak.com'dan ilan açıklamaları toplanır.

-Açıklamalar CSV dosyasına kaydedilir.

2.**Ön İşleme**

-Noktalama işaretleri ve durak kelimeleri temizlenir.

-Lemmatizasyon ve stem işlemleri uygulanarak iki ayrı dosyada temizlenmiş veriler kaydedilir.

3.**Zipf yasası kontrolü(Tercihen)**

-Kelime frekansları analiz edilerek doğal dile uygunluk kontrol edilir.

4.**Vektörleştirme**

-TF-IDF yöntemiyle ilan açıklamaları sayısal vektörlere dönüştürülür.

-Alternatif olarak Word2Vec modeli eğitilerek benzerlik ilişkileri oluşturulur.

5.**Benzerlik Hesaplama**

-TF-IDF için "cosine similarity" ile açıklamalar arası benzerlik oranları hesaplanır.

-Word2Vec ile kelimeler arası anlamsal yakınlık ölçülür.

6.**Sonuçların Analizi**

-Belirli bir eşik değeri üzerinde benzer ilan çiftleri tespit edilerek raporlanır.

## Veri Setinin Kullanılabileceği Amaçlar

- Aynı evin birden fazla ilana düşüp düşmediğini kontrol etme

- Emlak sitelerinde veri temizliği ve filtreleme

- İlan metinleri arasında anlamsal benzerlik analizleri yapma

- Doğal dil işleme projelerinde Türkçe veri örneği olarak değerlendirme

> 📎 Veri setine [buradan ulaşabilirsiniz](https://github.com/yuuyunie/emlak-projesi-ilan-aciklamasi-benzerlik-filtresi/blob/main/emlakjetodev.csv)

> Not: Veri yalnızca eğitim ve araştırma amaçlıdır. Ticari kullanımlar için ilgili web sitelerinin kullanım koşulları dikkate alınmalıdır.


## Gerekli Kütüphaneler ve Kurulum

-Aşağıdaki komutu terminale yazarak gerekli bütün kütüphaneleri tek seferde yükleyebilirsiniz.

pip install pandas numpy scikit-learn nltk gensim matplotlib

| Kütüphane                                    | Açıklama                                                                            |
| -------------------------------------------- | ----------------------------------------------------------------------------------- |
| [`pandas`](https://pandas.pydata.org/)       | CSV dosyalarının okunması ve veri çerçevesi işlemleri için kullanıldı.              |
| [`numpy`](https://numpy.org/)                | Sayısal işlemler, matris yapıları ve veri manipülasyonu için kullanıldı.            |
| [`scikit-learn`](https://scikit-learn.org/)  | TF-IDF vektörleştirme, cosine similarity hesaplama gibi işlemler için kullanıldı.   |
| [`nltk`](https://www.nltk.org/)              | Türkçe stopword temizliği, tokenizasyon ve lemmatizasyon işlemleri için kullanıldı. |
| [`gensim`](https://radimrehurek.com/gensim/) | Word2Vec modelinin eğitimi ve benzerlik analizleri için kullanıldı.                 |
| [`matplotlib`](https://matplotlib.org/)      | Zipf yasası analizi için log-log grafikleri çizmek amacıyla kullanıldı.             |

-Projeyi ilk kez çalıştırırken aşağıdaki Python kommutlarını bir kez çalıştırmanız yeterlidir.

import nltk

import requests

from nltk.tokenize import word_tokenize, sent_tokenize

from nltk.stem import WordNetLemmatizer, PorterStemmer

from nltk.corpus import stopwords

import csv

nltk.download('punkt')

nltk.download('stopwords')

nltk.download('wordnet')

nltk.download('avaraged_perceptron_tagger')

nltk.download('punkt_tab')

from sklearn.feature_extraction.text import TfidfVectorizer

import numpy as np

from sklearn.metrics.pairwise import cosine_similarity

import gensim

from gensim.models import Word2Vec

from nltk.stem import WordNetLemmatizer, PorterStemmer

from gensim.models import Word2Vec
