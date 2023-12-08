# AWS Sanallaştırma Projesi Dokümantasyonu

Bu dokümantasyon, Amazon AWS üzerinde gerçekleştirilen bir sanallaştırma projesinin adım adım uygulanışını içermektedir. Proje, kullanıcıların şifre güvenliğini analiz eden bir web tabanlı uygulamanın geliştirilmesini içermektedir. Ayrıca, bulut bilişim altyapısı ve Docker kullanılarak Windows işletim sistemindeki uygulama başarıyla bulutta sanallaştırılmıştır.

## Kurulum Adımları

1. **Amazon AWS Hesabı Oluşturun:**  
   [AWS](https://aws.amazon.com/) üzerinden bir hesap oluşturun.

2. **EC2 Dashboard'a Giriş Yapın:**  
   AWS ana sayfasında "EC2" seçeneğini belirleyin ve ardından "Launch Instance" butonuna tıklayın.
   
   ![EC2 Dashboard](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/936d24ab-20c1-44f1-8979-fbae6ede04c5)  

3. **Örnek Oluşturun:**  
   Amazon Linux Machine seçerek yeni bir örnek oluşturun.
   
   ![Örnek Oluştur](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/53821918-b645-485d-a521-42d196232399)  

4. **Anahtar Oluşturun:**  
   "Create new key pair" seçeneğine tıklayarak bir anahtar oluşturun ve .ppk uzantılı olarak kaydedin.  
   Not: Eğer .pem uzantılı bir anahtara sahipseniz, PuTTYgen kullanarak .ppk uzantısına dönüştürün.
   
   ![Anahtar Oluştur](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/731825e1-08e7-4f3f-9ef6-d1dac216adc8)
  
6. **HTTP ve HTTPS Protokollerine İzin Verin:**
   HTTP ve HTTPS protokollerini işaretleyip "Launch Instance" butonuna tıklayarak makine kurulumunu tamamlayın.
   
   ![Protokoller ve Başlatma](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/7a1a1902-cff6-4a26-b6bb-7a761cbfdc5e)

7. **PuTTY'i İndirin:**
    
   [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) adresinden PuTTY'i indirin ve kurun.
   
   Not: PuTTY aynı zamanda .pem uzantısını .ppk uzantısına dönüştürmek için PuTTYgen programını içermektedir.

8. **  .pem Uzantılı Anahtarı .ppk'ya Dönüştürün (Opsiyonel):**
    
   PuTTYgen uygulamasını başlatın, "Load private key" seçeneğiyle .pem uzantılı anahtarı yükleyin ve .ppk dosyasını kaydedin.

   
   ![PuTTYgen](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/b1eb3dd8-1dfa-4638-b33f-fb5d1693368f)
   

9. **PuTTY ile SSH Bağlantısı Kurun:**
   
    PuTTY'i başlatın, AWS'deki makinenizin Public IPv4 adresini girin, .ppk dosyasını ekleyin ve bağlantıyı kurun.
   
   ![PuTTY](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/c06a0762-9694-474a-b7c8-9240ca0a2771)

11. **Bilgisayardaki Dosyaları Makineye Yükleyin:**
 
    mkdir website
   
    cd website
   
    wget --no-check-certificate -r 'https://drive.google.com/uc?export=download&id=12xMi5wTIbRvaCNVgPdodLJgI2-TdxRSI' -O bulut.zip
   
    unzip bulut.zip

11. **Docker Kurun**

    sudo yum update -y
    
    sudo yum install docker -y
    
    sudo service docker start
    
    sudo usermod -aG docker ec2-user

12. **Dockerfile Oluşturun**

    vim Dockerfile
    
    İçeriğe geçmek için Insert tuşuna basın ve aşağıdaki içeriği ekleyin:
    
    ___
    
    FROM httpd
    
    COPY . /usr/local/apache2/htdocs/
    
    ___
    
    Çıkış yapmak için esc tuşuna basın :wq! yazın ve enter tuşuna basın.

14. **Docker Image Oluşturun ve Çalıştırın**

    docker build -t website .
    
    docker images
    
    docker run -itd -p 80:80 --name website website
    
    docker ps

**Websitenizi Kullanmaya Başlayın: Tarayıcınıza Public IPv4 adresini girerek websitenizi başarıyla kullanabilirsiniz.**


![website](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/eebd5900-3227-417c-8d99-d71ce830a849)

