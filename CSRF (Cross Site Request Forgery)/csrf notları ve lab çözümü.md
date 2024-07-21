<h1 align="center">IDOR (Insecure Direct Object Reference)</h1>

- **CSRF** zafiyeti bir saldırganın bir kullanıcıyı kandırarak bir linki açmasını, bir butona tıklamasını veya bir bağlantıya tıklamasını sağlamak suretiyle,
  kullanıcının hesabı üzerinde istemeden değişiklik yapmasına veya işlem gerçekleştirmesine olanak tanıyan bir güvenlik açığıdır.
  Bu zafiyet, herhangi bir web uygulamasında oturum açmış bir kullanıcının oturumunu, saldırganın o kullanıcıymış gibi işlemler yapmasına olanak sağlar.
  CSRF açıkları genellikle GET istekleri ve oturum yönetimi işlemlerinin doğru şekilde kontrol edilmemesinden kaynaklanır.
  Bu durum, saldırganın kullanıcı adına istek göndermesine ve yetkisiz işlemler yapmasına imkan tanır.
  Portswigger labları üzerinden konuyu işleyelim


  **Lab 1: CSRF vulnerability with no defenses :**
  - Lab da bize bir kullanıcı hesabı vermiş.Bizde o kullanıcı hesabı ile uygulamamıza giriş yapıyoruz.
   Giriş yaptıktan sonra maili csrf zafiyetini kullanarak değiştirmemizi istiyor. 
  
  ![](https://github.com/Yakup-uzn/Web-Security/blob/995f2612c5d3873e8439a284b7559af6718405ba/CSRF%20(Cross%20Site%20Request%20Forgery)/csrf%20ekran%20resimleri/1)

  -Hesaba giriş yaptık ve mailimizi değiştirmek için bir istek yolladık.Bu isteğimizi inceleyelim.

  
