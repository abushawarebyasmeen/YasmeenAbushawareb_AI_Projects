# SSS Asistanı - README

## Genel Bakış
Protel SSS Asistanı, kullanıcı sorgularına doğru ve hızlı yanıtlar vermek üzere tasarlanmış Django tabanlı zeki bir soru-cevap sistemidir.
Önceden tanımlanmış SSS veritabanı ile büyük dil modellerinin (LLM) gücünü birleştiren hibrit bir yaklaşım kullanır. Böylece kullanıcılar, 
soruları önceden yanıtlanmış olsa da gerçek zamanlı üretilmesi gerekse de en iyi yanıtı alır. 

---

## Özellikler

### 1. **SSS Veritabanı Sorgulama**
   - Sistem, sıkça sorulan sorular (SSS) ve karşılık gelen cevaplarından oluşan yapılandırılmış bir veritabanı tutar.(`sample_faqs.json` dosyasında toplanan Protel ile ilgili 190+ soru ve cevap.)  
   - Kullanıcı bir soru gönderdiğinde, sistem öncelikle semantik benzerlik teknikleri kullanarak veritabanında eşleşen soruyu arar.  
   - Eğer benzerlik skoru %90 veya üzerindeyse, ilişkili cevap kullanıcıya döner.  

### 2. **LLM Entegrasyonu**
   - Veritabanında eşleşen SSS bulunamazsa (benzerlik %90’ın altında ise), sistem bağlı olduğu Büyük Dil Modeli (LLM) ile dinamik olarak cevap üretir.  
   - Bu sayede veritabanında olmayan sorulara da doğru yanıt sağlanır.  
   - LLM, karmaşık, açık uçlu veya çok özel soruları da işleyebilir.  

### 3. **search_in_urls (Protel'e ait linklerde ariyor)**
   - LLM yeterli yanıt veremediğinde, sistem Protel web’den ilgili bilgileri çekebilir.  
   - Bu özellik, güncel veya Hazirkanan belgi harici bilgi gerektiren soruların doğruluğunu artırır.  

### 4. **Geliştirilmiş Benzerlik Skorlama Mekanizması**
   - Sistem artık daha gelişmiş NLP tabanlı benzerlik skorlama algoritması kullanır.  
   - Bu, sadece anahtar kelime eşleşmesi değil, anlamsal ilişkileri de dikkate alarak doğruluğu artırır.  

### 5. **Dinamik Bilgi Tabanı**
   - Yöneticiler, veritabanındaki SSS’leri kolayca ekleyip, düzenleyip, silebilir.  
   - SSS veritabanı, kullanıcı ihtiyaçlarına göre sürekli gelişecek şekilde tasarlanmıştır.  

### 6. **Cevapsız Sorgular İçin LLM Yedeği**
   - Soru veritabanında yoksa sistem otomatik olarak LLM’ye geçer ve ilgili, bağlama uygun cevap üretir.  
   - LLM cevap veremezse, Protel web search devreye girer.  
   - Hiç cevab bulamaz ise Nazikçe 'Üzgünüm cevab yok've 3 tane benzer konu olabılır sorular sonuyor.  
### 7. **Gelişmiş Sorgu Kayıtları**
   - Her sorgu ve onun yanıt kaynağı (SSS veritabanı, LLM, Wep) kayıt altına alınır.  
   - Bu sayede yöneticiler sistem doğruluğunu ve bilgi tabanını zamanla iyileştirebilir.  

### 8. **Etkileşimli Ön Yüz**
   - Basit ve kullanıcı dostu arayüz ile kullanıcılar sorularını yazıp cevaplarını görebilir.
   - Cevab bulamayınca benzer soru seçeneklerı sonuyor.  
   - Responsive tasarım sayesinde farklı cihazlarda sorunsuz çalışır.  

### 9. **Ölçeklenebilir Mimari**
   - Proje, küçük ölçekten kurumsal düzeye kadar genişleyebilir şekilde tasarlanmıştır.  

### 10. **Özelleştirilebilir Eşik Değerleri**
   - Yöneticiler benzerlik eşik değerini (varsayılan: %90) ayarlayarak hassasiyet ve kapsama arasında denge kurabilir.  

### 11. **Statik Dosya Desteği**
   - CSS, JavaScript ve görseller gibi statik dosyalar entegre edilmiştir; kullanıcı deneyimi zenginleştirilmiştir.  

---

## Sistem İşleyişi  
1. **Kullanıcı Sorgusu Gönderimi**:  
   - Kullanıcılar ön yüz üzerinden sorularını gönderir.  
2. **Veritabanı Araması**:  
   - Sistem, gönderilen sorunun tüm SSS’lerle benzerlik skorunu hesaplar.  
   - %90 veya üzeri benzerlikte eşleşme varsa, ilgili cevap getirilir.  
3. **LLM Yedeği**:  
   - Eşleşme bulunamazsa, soru gerçek zamanlı yanıt üretmek üzere LLM’ye gönderilir.  
4. **Cevap Gösterimi**:  
   - Kullanıcıya veritabanından veya LLM’den en iyi cevap sunulur.  
5. **Sorgu Kaydı**:  
   - Her sorgu ileride analiz ve geliştirme için kayıt altına alınır.  

---


## Avantajlar
- **Verimlilik**: Önceden kaydedilmiş SSS'lerle sık sorulan soruları hızlıca yanıtlar.
- **Esneklik**: LLM'ler sayesinde benzersiz veya beklenmeyen soruları da yanıtlayabilir.
- **Ölçeklenebilirlik**: Büyüyen veritabanlarına ve kullanıcı sayılarına kolayca uyum sağlar.
- **Kullanıcı Odaklı**: Sorunsuz ve sezgisel bir kullanıcı deneyimi sunar.
- **Özelleştirilebilir**: Yöneticiler sistem üzerinde kolayca ince ayar yapabilir.

---

## Kullanım Kılavuzu

### Kullanıcılar için
- Sorunuzu giriş kutusuna yazın ve "Soru Sor" butonuna basın.
- Eğer sorun tanınıyorsa, cevap anında görüntülenecektir.
- Tanınmayan sorular için, LLM’in cevap üretmesi için lütfen birkaç saniye bekleyin.
- Sorunuz için cevab yoksa, benzer olabilecek sorurar sunuyor, uygun soru varsa ona tıklayın
yoksa, başka soru sor butununa tıklayarak sorunuz başka kelimelerle sorabilirisiniz.

### Yöneticiler için
- Django’nun yönetici panelini kullanarak SSS veritabanını yönetin.
- Sorgu kayıtlarını düzenli olarak inceleyerek sık sorulan veya yanıtsız kalan soruları tespit edin.
- Veritabanını güncelleyerek sistem doğruluğunu ve kapsama alanını artırın.

---

## Projeyi Lokal Olarak Çalıştırma

### Gereksinimler
- Python (3.8 veya üstü)
- Django (4.x veya üstü)
- SQLite (varsayılan veritabanı, önceden yapılandırılmış)
- Opsiyonel: LLM entegrasyonu için API anahtarı (örneğin OpenAI veya benzeri)

### Adımlar
#Bu adimlari seçenek olarak anaconda prompot te çaliştirabilirsiniz.
1. Projeyi Klonlayın:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Sanal Ortam Kurulumu:
   ```bash
   python -m venv env
   source env/bin/activate   # On Windows: env\Scripts\activate
   ```

3. Bağımlılıkları Yükleyin:
   ```bash
   pip install -r requirements.txt
   ```

4. Ortam Değişkenlerini Yapılandırın:    #Projede Hazır var.
   - Proje kök dizinine .env dosyası oluşturun.
   - Aşağıdaki değişkenleri ekleyin:
     ```env
     SECRET_KEY=<your-django-secret-key>
     DEBUG=True
     LLM_API_KEY=<your-llm-api-key>
     ```

5. Veritabanı Migrasyonlarını Çalıştırın:  # manage.py dosyasina ulaşamazsanız dosyanın path=Yolu yazabilirsiniz
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

6. Örnek SSS Verilerini Yükleyin:
   - Örnek SSS’leri veritabanına yüklemek için bir script kullanabilirsiniz.
   - Örnek:
     ```bash
     python manage.py loaddata sample_faqs.json
     ```

7. Geliştirme Sunucusunu Başlatın:
   ```bash
   python C:\Users\yasme\Desktop\FQA\smart_FAQ\manage.py runserver
   ```
   - Uygulamaya `http://127.0.0.1:8000`.adresinden erişebilirsiniz.

8. Yönetici Paneline Erişin:  süper kullanıcı.txt dosyasinda yasmeenabushawareb giriş bilgilerine ulaşabirsiniz yada bu kod kullanarak yenisi yapabilir sınız.
   - Bir süper kullanıcı oluşturun:
     python manage.py createsuperuser
   - Yönetici paneline `http://127.0.0.1:8000/admin`adresinden erişebilirsiniz.
---

## Gelecekteki Geliştirmeler
- **Çok Dilli Destek**: Birden fazla dilde sorgu işleyebilme özelliği.
- **Gelişmiş Analitik**: Kullanıcı davranışı ve sistem performansına dair detaylı raporlar sunma.
- **İyileştirilmiş NLP Teknikleri**: Daha iyi benzerlik puanlaması için en yeni modellerin entegrasyonu.
- **Sesli Sorgu Entegrasyonu**: Kullanıcıların sesli giriş ile soru sorabilmesini sağlama.
- **Google Search API Entegrasyonu**: 
  - `google_search.py` dosyasındaki hazır SerpAPI google_search kullanan fonksiyonunu view dosyasına ekleyerek tekrar aktif edebiliriz.
  - Ancak Google araması aktifken, Protel dışı sorulara da cevap verildiği için anahtar kelime bazlı filtreleme önerilir.

---
## Kurulum ve Başlangıç
1. **Depoyu Klonlayın:**
   - Proje deposunu yerel sisteminize indirin veya klonlayın.

2. **Bağımlılıkları Yükleyin:**
   - `requirements.txt` dosyasında listelenen tüm gerekli bağımlılıkları `pip` ile yükleyin.

3. **Veritabanını Kurun:**
   - Django migration komutlarını çalıştırarak gerekli veritabanı tablolarını oluşturun.

4. **İlk Verileri Yükleyin:**
   - Veritabanını başlangıç FAQ kayıtları ile bir Python betiği ya da Django admin paneli kullanarak doldurun.

5. **Geliştirme Sunucusunu Başlatın:**
   - Sunucuyu yerel olarak başlatmak için `python manage.py runserver` komutunu kullanın.

6. **Uygulamaya Erişim:**
   - Web tarayıcınızda `http://127.0.0.1:8000` adresini açın.

---
## Folder Structure

```
smart_FAQ/
│-- db.sqlite3              # SQLite database file
│-- manage.py               # Django project management script
│-- .env                    # Environment variables file
│-- .gitignore              # Git ignore file
│-- README.md               # Project documentation
│--süper kullanıcı          # Enter to 'http://127.0.0.1:8000/admin' password
├── faq/                    # Main application directory
│   ├── __pycache__/        # Compiled Python files
│   ├── helper/             # Helper functions and utilities
│   ├── migrations/         # Database migrations
│   ├── __init__.py         # Package initialization
│   ├── admin.py            # Admin panel configuration
│   ├── apps.py             # Application configuration
│   ├── models.py           # Database models
│   ├── tests.py            # Unit tests
│   ├── views.py            # Application logic
│
├── smart_FAQ/              # Project settings directory
│   ├── __pycache__/        # Compiled Python files
│   ├── __init__.py         # Package initialization
│   ├── asgi.py             # ASGI configuration
│   ├── settings.py         # Project settings
│   ├── urls.py             # URL routing
│   ├── wsgi.py             # WSGI configuration
│
├── static/                 # Static assets
│   ├── styles.css          # CSS file for styling
│
├── templates/              # HTML templates
│   ├── ask.html            # User query page
│   ├── home.html           # Homepage
│
├── requirements.txt        # List of dependencies
├── Varified FAQ.py         # Script for verified FAQs

```

---
