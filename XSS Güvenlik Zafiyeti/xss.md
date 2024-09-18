<h1>AngularJS Nedir ve XSS Açığı Nasıl Çalışır</h1>
AngularJS, HTML kodu içinde çift küme parantezi kullanarak JavaScript ifadeleri çalıştırmanızı sağlar.

<div>{{ expression }}</div>

Bu kodda, expression ifadesi JavaScript'te geçerli bir ifade ise, AngularJS bunu değerlendirir ve sonucunu HTML'ye yerleştirir.
AngularJS'in çift küme parantezleri içinde doğrudan JavaScript ifadeleri yazabilirsiniz. Burada {{ }} ifadesinin içine bir JavaScript fonksiyonu yazılacak. $.on.constructor() ile yeni bir fonksiyon oluşturuluyor ve içerisine alert(1) yazılıyor. Bu, kullanıcıya bir uyarı penceresi gösterecek.

{{$on.constructor('alert(1)')()}}

Bu ifade AngularJS tarafından yorumlanacak ve JavaScript kodu çalıştırılacak. alert(1) fonksiyonu tetiklenerek XSS açığı kullanılmış olacak.

$on: AngularJS'in yerleşik fonksiyonlarından biridir ve olayları dinlemek için kullanılır.
constructor: JavaScript'teki fonksiyonların yapıcısıdır ve bu sayede yeni bir fonksiyon oluşturabilirsiniz.
alert(1): Tarayıcıda bir uyarı penceresi açmak için kullanılan JavaScript komutudur.

İkinci parantez çifti ise bu oluşturulan fonksiyonun hemen çalıştırılması anlamına gelir. JavaScript'te bir fonksiyon oluşturduktan sonra, onu çalıştırmak için hemen arkasına bir parantez eklemeniz gerekir.

Örneğin:
function myFunc() { return 42; }
myFunc();  // Bu fonksiyonu çalıştırır.


Benzer şekilde, $on.constructor('alert(1)') bir fonksiyon oluşturur, ancak bu fonksiyonu çalıştırmanız gerekir. İşte bu noktada ikinci parantez devreye girer:


<h1> XSS ve innerHTML </h1>

