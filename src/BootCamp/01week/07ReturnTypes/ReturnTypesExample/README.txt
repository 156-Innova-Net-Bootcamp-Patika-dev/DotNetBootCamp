# Sanal Pos Entegrasyon Projesi

### A��klama:

Sanal pos entegrasyon projesi �deme sa�lay�c�lar� veya bankalarla entegrasyon kurup �deme ve �deme sonras� i�lemleri yapabilmemizi sa�lamaktad�r.

#### Entegrasyonlarda a�a��daki i�levler yer almaktad�r;

* **auth**: M��teriden �cret �ekilmesini sa�lamaktad�r.
* **refund**: Ba�ar�yla ger�ekle�mi� bir �demenin m��teriye iadesini sa�lamaktad�r.
* **fetchRedirectionUrl**: M��terinin �deme sa�lay�c�s�n�n sayfas�na y�nlenebilece�i URL�i alabilmeyi sa�lar. Bu URL ile m��teri �deme sa�lay�c�n�n sayfas�na y�nelir. �demeyi bu sayfada ger�ekle�tirir.

Yukar�da sayd���m�z i�lemler projede her �deme sa�lay�c� i�in ayr� ayr� entegre edilir. Her �deme sa�lay�c� veya banka i�in ayr� entegrasyon yap�l�r. Yap�lan entegrasyonlar� kullanabilmek i�in REST katman� olu�turulmu�tur. Verilen Dotnet projesinde �Sofort�, �Est� gibi �deme sa�lay�c�lara ait entegrasyonlar **tamamlanm�� durumdad�r.**

#### Projedeki �deme Sa�lay�c�lar ve Bankalar;

* **Adyen**: Yurtd��� �demelerinde �deme ile ilgili i�lemlerin yap�labilmesini sa�layan �deme sa�lay�c�d�r. Sofort ve Paypal isminde iki �deme y�ntemi sunmaktad�r.

* **Est**: Kartl� i�lemler yoluyla �deme ile ilgili i�lemlerin yap�labilmesini sa�layan �deme sa�lay�c�d�r.

* **TyBank**: Kartl� i�lemler yoluyla �deme ile ilgili i�lemlerin yap�labilmesini sa�layan bankad�r.

#### Projede a�a��daki i�lemler tamamlanm��t�r;

* Est �deme sa�lay�c�s�na ait �auth�, �refund� i�levleri entegre edilmi�tir. Est sa�lay�c�s� �fetchRedirectionUrl� i�levi desteklememektedir.
* Adyen �deme sa�lay�c�s� alt�ndaki �Sofort� �deme y�ntemine ait �refund� ve �fetchRedirectionUrl� i�levleri entegre edilmi�tir. �Sofort� �deme y�ntemi �auth� i�levi desteklememektedir.
* Tamamlanan entegrasyonlara ait Request/Response s�n�flar� haz�rlanm��t�r.
* Yap�lan sanal pos entegrasyonlar�n� kullanabilmek i�in REST katman� haz�rlanm��t�r.
* Tamamlanan entegrasyonlara ait birim testleri yaz�lm��t�r.


#### Yap�lmas� istenenler:

1 - Paypal �deme y�ntemine ait �PaypalPosService� s�n�f�ndaki �fetchRedirectionUrl� i�levinin entegrasyonu sizin taraf�n�zdan tamamlanmal�d�r.
�RedirectUrlRequest� veri modelindeki alanlar doldurulur. �https://www.adyen.com/api/v1/sofort/redirection/url� adresine HTTP POST iste�i at�l�r.
Gelen cevapta �url�, �rawBody� alanlar� yer almaktad�r.

2 - TyBank�a ait �TyBankPosService� s�n�f�ndaki �refund� i�levi sizin taraf�n�zdan tamamlanmal�d�r.
�refund� i�leminde �RefundRequest� veri modelindeki alanlar doldurulur. �https://www.tybank.com/pos/api/v1/tybank/refund � adresine HTTP POST iste�i at�lmal�d�r.
Gelen cevab� �TyBankRefundResponse� ile modelleyiniz. S�n�fa ait alanlar a�a��daki gibidir.
�response�, �errorCode�, �message�

3 - TyBank�a ait �TyBankPosService� s�n�f�ndaki �auth� i�levi sizin taraf�n�zdan tamamlanmal�d�r.
�auth� i�leminde �AuthRequest� veri modelindeki alanlar doldurulur. �https://www.tybank.com/pos/api/v1/tybank/auth � adresine HTTP POST iste�i at�lmal�d�r.
Gelen cevab� �TyBankAuthResponse� ile modelleyiniz. S�n�fa ait alanlar a�a��daki gibidir.
�response�, �authCode�, �transactionId�, �errMsg�

4 - Projede �nceden yaz�lm�� kodlar da dahil olmak �zere SOLID, Clean Code, OOP prensipleri a��s�ndan her t�rl� refactoring i�lemini ger�ekle�tirmeniz beklenmektedir.

5 - Projede yeni yap�lacak entegrasyonlara ait birim testlerini yazman�z gerekmektedir.
