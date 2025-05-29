# Emlak İlanları Eşleştirme Uygulaması

Bu proje, emlak ilanlarını metin benzerlik analizi yöntemleriyle eşleştirmek için geliştirilmiştir. TF-IDF ve Word2Vec modelleri (CBOW ve Skip-gram) kullanılarak, verilen bir emlak ilanıyla en benzer ilanlar bulunur. Proje, doğal dil işleme (NLP) tekniklerini kullanarak anlamsal benzerlikleri değerlendirir, sıralama tutarlılığını Jaccard benzerlik matrisi ile analiz eder ve detaylı bir rapor sunar.

# Projenin Amacı ve Özellikleri

- **Metin Benzerlik Analizi**: TF-IDF ve 16 farklı Word2Vec modeli ile emlak ilanları arasında benzerlik hesaplanır.
- **Anlamsal Değerlendirme**: Modellerin sonuçları 1-5 arası puanlarla değerlendirilir.
- **Sıralama Tutarlılığı**: 18 modelin tutarlılığı Jaccard matrisi ile analiz edilir.
- **Raporlama**: Analizler `semantic_report.pdf` dosyasında detaylı bir şekilde sunulur.

# Kurulum ve Bağımlılıklar

# Gereksinimler
- Python 3.8 veya üzeri
- Jupyter Notebook

# Bağımlılıkları Yükleme
Aşağıdaki komutla gerekli kütüphaneleri yükleyin, eğer kütüphaneleri yüklemekte sıkıntı yaşıyor iseniz bashinize pip install komutunu yazarak olmayan kütüphanelerini bilgisayarınıza yükleyin.

```bash
import pandas as pd
from gensim.models import Word2Vec
import nltk
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.corpus import stopwords
from tqdm import tqdm
from snowballstemmer import TurkishStemmer
import zeyrek
import re
import logging
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
import gensim
from gensim.models import Word2Vec
from nltk.stem import WordNetLemmatizer, PorterStemmer
from gensim.models import Word2Vec
from itertools import combinations

```

# Veri ve Model Dosyalarını Hazırlama
Aşağıdaki dosyaları repodaki ana dizine yerleştirin:
- `emlakodev.csv`: Ham emlak ilanları veri seti
- `lemmatized_sentences.csv`: Lemmatize edilmiş cümleler
- `stemmed_sentences.csv`: Stem edilmiş cümleler
- `tfidf_lemmatized.csv`: Lemmatize edilmiş TF-IDF matrisi
- `tfidf_stemmed.csv`: Stem edilmiş TF-IDF matrisi
- `*.model`: Word2Vec modelleri (örneğin, `lemmatized_model_cbow_window2_dim100.model`, toplam 16 dosya)

**Not:** Model dosyaları büyük olabilir ve `.gitignore` ile dışlanmış olabilir. Bu durumda, [link] adresinden indirebilirsiniz (linki ekle).

1. Repoyu klonlayın
git clone https://github.com/yuuyunie/emlak-ilanlari-eslestirme-uygulamasi.git
cd emlak-ilanlari-eslestirme-uygulamasi
2. Bağımlılıkları yükleyin (yukarıdaki adımı takip edin).
3. Veri dosyalarını ve Word2Vec modellerini ana dizine yerleştirin.
4. Jupyter Notebook’u başlatın:
   ```bash
   jupyter notebook
   ```
5. emlak_projesi_2.ipynb dosyasını açın ve tüm hücreleri sırayla çalıştırın.
6. Çıktılar şu dosyalarda kaydedilecektir:
   -word2vec_results.txt: Word2Vec modellerinin benzerlik sonuçları
   -semantic_scores.txt: Anlamsal değerlendirme puanları
   -semantic_results_table.txt: LaTeX tablosu
   -semantic_comments.txt: Anlamsal değerlendirme yorumları
   -jaccard_matrix.txt: Jaccard benzerlik matrisi
   -jaccard_comments.txt: Jaccard analizi yorumları
   
#Dosya Yapısı
-emlak_projesi_2.ipynb: Ana analiz kodları ve iş akışı
-emlakodev.csv: Ham veri seti (emlak ilanları)
-lemmatized_sentences.csv: Lemmatize edilmiş cümleler
-stemmed_sentences.csv: Stem edilmiş cümleler
-tfidf_lemmatized.csv: Lemmatize edilmiş TF-IDF matrisi
-tfidf_stemmed.csv: Stem edilmiş TF-IDF matrisi
-*.model: 16 adet Word2Vec model dosyası (örneğin, -lemmatized_model_cbow_window2_dim100.model)
-word2vec_results.txt: Benzerlik analiz sonuçları
-semantic_scores.txt: Anlamsal puanlar
-semantic_results_table.txt: Anlamsal değerlendirme tablosu (LaTeX)
-semantic_comments.txt: Anlamsal yorumlar (LaTeX)
-jaccard_matrix.txt: Jaccard matrisi (LaTeX)
-jaccard_comments.txt: Jaccard yorumları (LaTeX)
-semantic_report.docx: Detaylı analiz raporu (Word)
-semantic_report.pdf: Detaylı analiz raporu (PDF)
-trainmodel.py: Word2Vec modellerini eğitmek için yardımcı script (opsiyonel)

#Rapor ve Bulgular
Analizlerin detaylı özeti semantic_report.pdf dosyasında yer alır. Rapor, yöntemleri, sonuçları (TF-IDF, Word2Vec, Jaccard analizi) ve kod açıklamalarını içerir. Dosyayı incelemek için açabilirsiniz.

#Katkıda Bulunma
Proje açık kaynaktır. Katkıda bulunmak için pull request gönderin veya sorunları bildirin. Önerilere her zaman açığım!
