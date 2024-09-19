<h1>AngularJS Nedir ve XSS Açığı Nasıl Çalışır</h1>
AngularJS, HTML kodu içinde çift küme parantezi kullanarak JavaScript ifadeleri çalıştırmanızı sağlar.

```html
<div>{{ expression }}</div>
```

Bu kodda, expression ifadesi JavaScript'te geçerli bir ifade ise, AngularJS bunu değerlendirir ve sonucunu HTML'ye yerleştirir.
AngularJS'in çift küme parantezleri içinde doğrudan JavaScript ifadeleri yazabilirsiniz. Burada {{ }} ifadesinin içine bir JavaScript fonksiyonu yazılacak. $.on.constructor() ile yeni bir fonksiyon oluşturuluyor ve içerisine alert(1) yazılıyor. Bu, kullanıcıya bir uyarı penceresi gösterecek.

```javascript
{{$on.constructor('alert(1)')()}}
```
Bu ifade AngularJS tarafından yorumlanacak ve JavaScript kodu çalıştırılacak. alert(1) fonksiyonu tetiklenerek XSS açığı kullanılmış olacak.

$on: AngularJS'in yerleşik fonksiyonlarından biridir ve olayları dinlemek için kullanılır.
constructor: JavaScript'teki fonksiyonların yapıcısıdır ve bu sayede yeni bir fonksiyon oluşturabilirsiniz.
alert(1): Tarayıcıda bir uyarı penceresi açmak için kullanılan JavaScript komutudur.

İkinci parantez çifti ise bu oluşturulan fonksiyonun hemen çalıştırılması anlamına gelir. JavaScript'te bir fonksiyon oluşturduktan sonra, onu çalıştırmak için hemen arkasına bir parantez eklemeniz gerekir.

Örneğin:
```javascript
function myFunc() { return 42; }
myFunc();  // Bu fonksiyonu çalıştırır.
```javascript

Benzer şekilde, $on.constructor('alert(1)') bir fonksiyon oluşturur, ancak bu fonksiyonu çalıştırmanız gerekir. İşte bu noktada ikinci parantez devreye girer:


<h1> XSS ve innerHTML </h1>

innerHTML, bir HTML elementinin içeriğini dinamik olarak değiştiren bir JavaScript özelliğidir. Kullanıcı girişlerini veya herhangi bir veri parçasını bir elementin içine HTML olarak yerleştirmek için kullanılır.

document.getElementById("example").innerHTML = "<script>alert('XSS');</script>";

Bu örnek, example ID'li HTML elementinin içeriğini değiştirecektir. Eğer dinamik olarak bir kullanıcı girdisini HTML olarak ekleyecek olursanız, XSS saldırılarına açık hale gelebilirsiniz.

<h3>innerHTML İçine <script> Tagi Koymak </h3>

Tarayıcılar, güvenlik ve performans nedenlerinden dolayı, innerHTML kullanılarak sonradan sayfaya eklenen <script> taglerini otomatik olarak çalıştırmaz. Bu, tarayıcıların bilinçli bir güvenlik önlemidir. Dinamik olarak eklenen <script> etiketleri doğrudan çalışmaz, bu yüzden kötü niyetli bir kullanıcının XSS açığından faydalanması bu yolla engellenmeye çalışılır.

Bu davranış, XSS saldırıları bağlamında oldukça önemlidir çünkü tarayıcılar bu tür saldırıları kısmen önleyebilmek için <script> taglerini dinamik olarak çalıştırmamayı seçmiştir. Ancak bu, XSS saldırılarının tamamen önüne geçmez. Saldırganlar hala başka yollarla zararlı JavaScript kodu çalıştırabilir. Örneğin:

Event Handlers: Dinamik olarak bir HTML elementine onclick, onmouseover, vb. gibi olay dinleyicileri eklenebilir. Örnek:

```html
document.getElementById("example").innerHTML = "<img src='x' onerror='alert(1)'>";
```
Bu örnekte, bir resim etiketi <img> ekleniyor ve resim yüklenemediğinde onerror olayı tetiklenerek alert(1) çalıştırılıyor.



<h1>Escape (Kaçış Karakterleri Kullanma)</h1>

"Escape" (kaçış), özel karakterlerin yanlış yorumlanmasını engellemek için, bu karakterleri farklı biçimlerde ifade etmektir. Örneğin, HTML, JavaScript, URL gibi ortamlarda bazı karakterler özel bir anlam taşır (örn: <, >, ", &). Bu karakterlerin ham haliyle kullanılması güvenlik riskleri doğurabilir veya beklenmeyen davranışlara neden olabilir. Escape, bu karakterlerin özel anlamını kaybettirerek onları güvenli hale getirir.

Örnek 1: HTML Escape
HTML belgelerinde <, > gibi karakterler etiket anlamı taşır. Bu karakterlerin kullanıcı tarafından sağlanan içeriklerde kullanılması, Cross-Site Scripting (XSS) gibi saldırılara neden olabilir.

Problemi Gösterme:

```javascript
<p>Kullanıcı Yorum: <script>alert("XSS Saldırısı!");</script></p>
```
Yukarıdaki kodda, kullanıcının yazdığı yorumda bir <script> etiketi varsa, bu doğrudan çalışır ve bir XSS saldırısına neden olabilir. Bu tür karakterleri kaçırmak (escape) bu riski ortadan kaldırır.

Çözüm:

```javascript
<p>Kullanıcı Yorum: &lt;script&gt;alert("XSS Saldırısı!");&lt;/script&gt;</p>
```
Bu durumda, < ve > işaretleri &lt; ve &gt; olarak escape edildi. Tarayıcı, bu karakterleri HTML etiketleri olarak değil, düz metin olarak algılar.

Örnek 2: JavaScript Escape
JavaScript'te de " veya ' karakterleri, string sınırları anlamına gelir ve yanlış yerlerde kullanılırsa hata veya güvenlik riski oluşturabilir.

Problemi Gösterme:

```javascript
let userInput = '"; alert("XSS");';
let script = `<script>let data = "${userInput}";</script>`;
document.write(script);
```
Yukarıdaki JavaScript kodu, kötü niyetli bir kullanıcının girdiği "; alert("XSS"); karakterleri sayesinde bir XSS saldırısına açık hale gelir.

Çözüm: Kaçış karakterleriyle bu sorunu çözebiliriz:

```javascript
let userInput = '\"; alert(\"XSS\");';
let script = `<script>let data = "${userInput}";</script>`;
document.write(script);
```
Bu kodda, " işareti kaçırılarak (escaped) JavaScript tarafından string sınırı olarak algılanmaz ve saldırı önlenir.



<h1>Encode (Kodlama)</h1>
"Encode" (kodlama), verilerin farklı ortamlarda güvenli şekilde taşınması veya işlenmesi için kullanılan bir tekniktir. Kodlama, verinin belirli bir formatta yeniden düzenlenmesi anlamına gelir ve bu genellikle veri taşırken veya iletilirken veri bütünlüğünü korur. Web geliştirmede sıkça kullanılan birkaç encode türü şunlardır:

Örnek 1: URL Encode
URL'ler yalnızca belirli bir karakter kümesini destekler ve bazı karakterler URL'de kullanılamaz. URL encoding (yüzde kodlama) bu karakterlerin URL içinde güvenli bir şekilde taşınabilmesi için onları dönüştürür.

Problemi Gösterme: Eğer bir URL'nin parçası olarak bir boşluk veya diğer özel karakterler kullanmak isterseniz, bu karakterler URL'de sorun yaratabilir.

Örneğin:

```text
https://example.com/search?query=ali&veli
```
Yukarıdaki URL'de boşluk ya da & işareti problem yaratabilir. & işareti, URL'de parametre ayırıcı olarak kullanılır, bu yüzden bu karakteri olduğu gibi kullanmak URL'nin yanlış anlaşılmasına neden olabilir.

Çözüm: Bu karakterleri encode ederek URL'de güvenli hale getirebiliriz:

```text
https://example.com/search?query=ali%20%26%20veli
```
Burada:

Boşluk %20 ile,
& ise %26 ile kodlanmıştır.

<h3>Örnek 2: Base64 Encode</h3>
Base64 kodlama, ikili verileri metin formatında güvenli bir şekilde taşımak için kullanılır. Özellikle e-posta, HTTP başlıkları gibi yerlerde sıkça tercih edilir. Base64, veriyi ASCII karakterleriyle taşır.

Problemi Gösterme: Bir resim dosyasını e-posta ile gönderirken, dosya binary (ikili) formatında olduğu için taşıma sorunları yaşanabilir.

Çözüm: Base64 kodlama, bu ikili veriyi metne çevirerek güvenli bir şekilde taşımanızı sağlar:

```bash
Input: Hello
Base64 Encoded: SGVsbG8=
```
Hello kelimesi, Base64 ile kodlanmış haliyle SGVsbG8= olur. Bu şekilde taşınan veri, herhangi bir format sorunu olmadan taşınabilir.












