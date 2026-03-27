<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>İklimPedia</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f6f9;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background: white;
      padding: 30px;
      border-radius: 15px;
      width: 400px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
    }

    h1 {
      text-align: center;
      color: #2c7a7b;
    }

    h2 {
      text-align: center;
      color: #2c7a7b;
      font-size: 16;
    }

    input {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      margin-top: 10px;
    }

    button {
      width: 100%;
      margin-top: 10px;
      padding: 10px;
      background: #2c7a7b;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    .result {
      margin-top: 20px;
      background: #edf7f7;
      padding: 15px;
      border-radius: 10px;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>İklim Pedia</h1>
  <h1>(Ad Vikipedia'dan gelmiştir)</h1>
  <input type="text" id="search" placeholder="Bir iklim terimi yaz...">
  <button onclick="ara()">Ara</button>

  <div class="result" id="sonuc"></div>
</div>

<script>
let veriler = {
  "sera etkisi": "Atmosferdeki gazların ısıyı tutarak Dünya'nın sıcaklığını artırmasıdır.",
  "küresel ısınma": "Dünya'nın ortalama sıcaklığının zamanla artmasıdır.",
  "iklim değişikliği": "Uzun vadeli hava koşullarında meydana gelen değişikliklerdir.",
  "iklim": "Uzun yıllar boyunca gözlemlenen hava olaylarının ortalamasıdır.",
  "hava durumu": "Kısa süreli atmosfer olaylarıdır.",
  "karbon ayak izi": "Bir kişinin doğaya saldığı karbon miktarıdır.",
  "fosil yakıt": "Kömür, petrol ve doğalgaz gibi yakıtlardır.",
  "yenilenebilir enerji": "Güneş, rüzgar gibi tükenmeyen enerji kaynaklarıdır.",
  "ozon tabakası": "Güneşin zararlı ışınlarını engelleyen atmosfer tabakasıdır.",
  "kuraklık": "Uzun süre yağış olmaması durumudur.",
  "sel": "Aşırı yağış sonucu su taşkını oluşmasıdır.",
  "erozyon": "Toprağın rüzgar veya su ile taşınmasıdır.",
  "buzul erimesi": "Küresel ısınma nedeniyle buzulların küçülmesidir.",
  "deniz seviyesi yükselmesi": "Buzulların erimesiyle deniz seviyesinin artmasıdır.",
  "rüzgar enerjisi": "Rüzgarın gücünden elde edilen enerjidir.",
  "güneş enerjisi": "Güneşten elde edilen enerjidir.",
  "hidroelektrik": "Suyun gücüyle elektrik üretilmesidir.",
  "karbon döngüsü": "Karbonun doğada sürekli hareket etmesidir.",
  "iklim krizi": "İklim değişikliğinin ciddi boyutlara ulaşmasıdır.",
  "atmosfer": "Dünya'yı çevreleyen gaz tabakasıdır."
  "biyoçeşitlilik": "Bir ekosistemdeki canlı türlerinin sayıca zenginliğidir.",
  "sürdürülebilirlik": "Doğal kaynakların dengeli ve gelecek odaklı kullanımıdır.",
  "net sıfır": "Salınan sera gazı ile emilenin eşitlenmesi durumudur.",
  "karbon yutağı": "Atmosferdeki karbonu emen orman veya okyanus alanlarıdır.",
  "sıfır atık": "İsrafın önlenmesi ve atıkların geri kazanılması felsefesidir.",
  "mikroplastik": "Çevreyi kirleten 5mm'den küçük plastik parçalarıdır.",
  "su ayak izi": "Kullanılan toplam tatlı su miktarının ölçüsüdür.",
  "döngüsel ekonomi": "Kaynakların geri dönüştürülerek sürekli kullanıldığı sistemdir.",
  "metan gazı": "Isıyı hapsetme gücü yüksek bir sera gazıdır.",
  "asit yağmuru": "Fosil yakıt dumanlarının yağışla birleşerek asidik özellik kazanmasıdır."
  "ekolojik ayak izi": "İnsan faaliyetlerinin doğa üzerindeki toplam etkisinin ölçüsüdür.",
  "yeşil badana": "Bir kurumun aslında çevreci olmadığı halde kendini öyle gösterme çabasıdır.",
  "yeniden yabanıllaştırma": "Bozulmuş ekosistemlerin doğal süreçlerine geri döndürülmesidir.",
  "karbon yakalama": "Atmosferdeki karbondioksitin teknolojik yöntemlerle tutulup depolanmasıdır.",
  "paris iklim anlaşması": "Küresel ısınmayı 1.5 derece ile sınırlandırmayı hedefleyen uluslararası anlaşmadır.",
  "orman devşirme": "Ormanlık alanların tarım veya yerleşim için yok edilmesidir (Deforestasyon).",
  "permafrost": "En az iki yıl üst üste donmuş halde kalan toprak tabakasıdır.",
  "biyogaz": "Organik atıkların oksijensiz ortamda çürümesiyle oluşan yanıcı gazdır.",
  "kompost": "Bitkisel ve hayvansal atıkların doğal yolla gübreye dönüşmesidir.",
  "agroekoloji": "Tarımı doğal ekosistem süreçleriyle uyumlu hale getiren bilim dalıdır.",
  "çevresel adalet": "Çevresel yüklerin tüm insanlar arasında eşit ve adil dağılmasıdır.",
  "ısıl ada etkisi": "Şehirlerin kırsal alanlara göre daha sıcak olması durumudur.",
  "istilacı türler": "Geldikleri yeni ekosisteme zarar veren yerli olmayan canlılardır.",
  "deniz asitlenmesi": "Okyanusların fazla CO2 emmesi sonucu pH seviyesinin düşmesidir.",
  "karbon vergisi": "Sera gazı salımı yapan faaliyetlere uygulanan mali yükümlülüktür."
};

function ara() {
  let kelime = document.getElementById("search").value.toLowerCase().trim();
  let sonuc = document.getElementById("sonuc");

  if (veriler[kelime]) {
    sonuc.innerHTML = `
      <strong>${kelime.toUpperCase()}</strong><br><br>
      ${veriler[kelime]}
    `;
  } else {
    sonuc.innerHTML = "Bu terim bulunamadı 😔";
  }
}
</script>

</body>
</html>
