<h1 align="center">XML NEDİR?</h1>

**XML (eXtensible Markup Language)**, bilgisayar sistemleri arasında veri değişimini kolaylaştırmak amacıyla tasarlanmış bir işaretleme dilidir. XML, verilerin yapısını ve taşınabilirliğini tanımlamada kullanılır ve HTML'e benzer şekilde etikete dayalı bir dildir. Ancak, XML'in HTML'den farkı, veri sunumu yerine verilerin taşınması ve depolanmasına odaklanmasıdır.

## HTML ve XML Arasındaki Farklar ve XML'in Kullanım Alanları 
HTML (HyperText Markup Language), web sayfalarının yapısını ve içeriğini tanımlamak için kullanılır ve temel amacı, metin, görseller, bağlantılar ve diğer medya türlerini biçimlendirerek web tarayıcılarında nasıl görüneceğini belirlemektir. Örneğin, h1 etiketi büyük bir başlık oluştururken, p etiketi bir paragraf oluşturur. HTML, verilerin sunumuna odaklanırken, XML (eXtensible Markup Language) verilerin taşınması ve depolanması için tasarlanmış bir dildir. XML, verinin anlamını ve yapısını tanımlar, ancak verinin nasıl görüneceği konusunda herhangi bir bilgi içermez. XML verileri HTML’ye dönüştürüldükten sonra bir web tarayıcısında görüntülenebilir. Duyarlı bir web sitesi oluşturmak istiyorsanız, bu bir gerekliliktir.

Örneğin, hava durumu tahminleri veya haber akışları gibi zaman içinde güncellenen verileriniz varsa, bu verileri depolamak için XML kullanabilirsiniz. Bir kullanıcı web sitenizi ziyaret ettiğinde XML verileri HTML’ye dönüştürülür ve sayfada görüntülenir. Sadece HTML kullanırsanız, her veri değişikliğinde web sayfasını elle güncellemeniz gerekir. Bu çok zaman alıcı ve hata yapmaya açık bir yöntemdir. Ancak XML kullanarak, veriler ve sunum ayrı tutulur, yani veriler otomatik olarak güncellenir ve web sayfanızda anında gösterilir. Bu, web sitenizi yönetmeyi ve güncellemeyi çok daha kolay hale getirir. HTML, web içeriğinin nasıl görüneceğine odaklanırken, XML verilerin ne anlama geldiğine odaklanır.

## Temel XML yapısı

 XML belgeleri, bir kök eleman ve onun içinde yer alan alt elemanlardan oluşur. Her eleman bir açılış etiketi <etiket> ve kapanış etiketi </etiket> ile belirtilir. Örneğin, aşağıdaki basit XML belgesi, bir kütüphanedeki kitapları listeler:

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<kitaplik>
    <kitap>
        <baslik>Bir Roman</baslik>
        <yazar>Yazar Adı</yazar>
        <yayinyili>2023</yayinyili>
        <fiyat>30.00</fiyat>
    </kitap>
    <kitap>
        <baslik>Başka Bir Roman</baslik>
        <yazar>Başka Bir Yazar</yazar>
        <yayinyili>2022</yayinyili>
        <fiyat>25.00</fiyat>
    </kitap>
</kitaplik>

```

Bu örnekte, <kitaplik> kök elemanıdır ve iki adet <kitap> alt elemanı içerir. Her kitap elemanı, başlık, yazar ve yayın yılı bilgilerini taşır. XML, verilerin yapısını ve anlamını belirlemeye yarar, ancak verilerin nasıl görüneceğini belirtmez.







