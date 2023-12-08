# AWS-Sanallastirma-Projesi
Bu proje, Amazon AWS üzerinde gerçekleştirilen bir sanallaştırma örneğinin nasıl uygulanacağını içermektedir. Kullanıcıların şifre güvenliğini analiz eden bir web tabanlı uygulama geliştirilmiştir. Proje kapsamında, bulut bilişim altyapısı ve Docker kullanılarak uygulama sanallaştırılmıştır..

## Kurulum Adımları

1. **Amazon AWS Kayıt Ol**: [AWS](https://aws.amazon.com/) üzerinden hesap oluşturun.
2. **Dashboard EC2 seç**:AWS ana sayfasına geldikten sonra EC2 seçeneğini seçin ardından Launch Instance butonuna tıklayın
![Dashboard EC2 seç](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/936d24ab-20c1-44f1-8979-fbae6ede04c5)
3. **Instances Oluştur**: Amazon Linux Machine seçerek yeni bir örnek oluşturun.
![Instances Oluştur](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/53821918-b645-485d-a521-42d196232399)
4. **Key Oluşturun**: Create new key pair tuşuna tıklayın ve ardından keyinize isim verip .ppk şeklinde keyinizi oluşturun.
![Key Oluştur](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/731825e1-08e7-4f3f-9ef6-d1dac216adc8)

Not: Eğer ppk yerine hazırda bir .pem uzantılı bir keyiniz varsa bu .pem uzantılı keyi .ppk uzantısına dönüştürmek için PuTTYgen kullanılacaktır.

5. **HTTP ve HTTPS protokollerine izin verme**: HTTP ve HTTPS protokollerinin tiklerini işaretleyip Launch Instance butonuna tıklayarak makine kurulumumuzu bitirin. Yaklaşık olarak 10-15 saniye sonra makineniz kullanıma hazır hale gelicektir.
![Protokoller ve Başlatma](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/7a1a1902-cff6-4a26-b6bb-7a761cbfdc5e)
6.**PuTTY indir**: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html adresinden PuTTY indirelim ve kuralım.  
Not: PuTTY uygulamasıyla birlikte .pem uzantısını değiştirebileceğimiz PuTTYgen programı da kurulmaktadır.
7.**Dosyanınz .pem uzantılı değil ise bu aşamayı atlayınız**: PuTTYgen uygulamasını başlatın ve File butonundan Load private key butonunu seçin. Daha sonra çıkan pencerede tamam'a tıklayıp Save Private Key butonuna tıklayın .ppk dosyanız hazır.
![PuTTYgen 1](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/b1eb3dd8-1dfa-4638-b33f-fb5d1693368f)
![PuTTYgen 2](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/ce94c95a-6d2c-49a2-ad78-26e6566a4f39)
8. **PuTTY Kullanarak SSH Bağlantısı**: EC2 instance'a SSH ile bağlanmak için PuTTY kullanın. PuTTY uygulamasını başlatıp AWS'deki makinenizin Public IPv4 adresini girin. Daha sonra Connections > SSH > AUTH > Credentials kısmından .ppk dosyamızı import edin. Session ekranına geri dönüp isterseniz her seferinde aynı aşamaları tek tek yapmamak için Saved Session kısmına isim verip save diyerek kaydedin ve Open diyerek başlatın. Gelen terminal ekranına user kısmına ec2-user diyip enter'a basın.
![PuTTY](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/c06a0762-9694-474a-b7c8-9240ca0a2771)
9. **Bilgisayardaki dosyaları makineye yüklemek**:
**mkdir website**

**cd website**

yüklemek kolay olsun diye tüm websitesi kodlarını google drive üzerine bulut.zip adıyla yüklemiştim bununda paylaşma bağlantısını kopyalayıp aşağıdaki formatı değiştirip kullanabilirsiniz.

**wget --no-check-certificate -r 'https://drive.google.com/uc?export=download&id=12xMi5wTIbRvaCNVgPdodLJgI2-TdxRSI' -O bulut.zip**

**unzip bulut.zip**

11. **Docker kurulumu**: 
sudo yum update -y

sudo yum install docker -y

sudo service docker start

sudo usermod -aG docker ec2-user 

![Docker install](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/46f715c2-d4c3-47c4-a561-5877f5e18795)

13. **Dockerfile Oluştur**:
**vim Dockerfile** komutunu yazalım ve vim metin editörü ekranına girelim yazma moduna geçmezse Insert tuşuna basın.

FROM httpd

COPY . /usr/local/apache2/htdocs/

esc tuşuna bastıktan sonra :wq! yazıp enter'a bastıktan sonra vim editöründen çıkış yapın.

15. **Docker Image Oluştur ve Çalıştır**:
docker build -t website .

docker images

docker run -itd -p 80:80 --name website website

docker ps

![Docker Image](https://github.com/AndacAkyuz/AWS-Sanallastirma-Projesi/assets/91327557/5a18450a-f98b-471c-8447-64ebe95779ea)


**Public IPv4 adresini tarayınıza girip websitenizi başarıyla kullanabilirsiniz**

