<h1 align="center">
Nöbetçi Eczane API<a name="readme-top"></a>
</h1>

<div align="center">
  <img src="./Readme Resources/Duty Pharmacy API Logo.png" alt="Logo" width="120"/>
</div>

## İçindekiler

- [API Hakkında](#api-hakkında)
- [Dokümantasyon](#dokümantasyon)
- [İstek Örnekleri](#i̇stek-örnekleri)
- [Lisans](#lisans)
- [İletişim](#i̇letişim)


![—————————————————————————————————————————————————](./Readme%20Resources/Line.png)

## API Hakkında

Bu repo, Türkiye'deki nöbetçi eczaneleri sunan API'nin dokümantasyonunu içerir.

HTTP GET istekleriyle `il`, `ilce` ve `api_key` parametrelerini alır
ve istenilen şehirdeki nöbetçi eczaneleri JSON formatında sağlar.


![—————————————————————————————————————————————————](./Readme%20Resources/Line.png)

## Dokümantasyon

Base URL: `https://toktasoft.com/api/duty-pharmacy`

API 3 farklı parametre almaktadır.

| Parametre                       | Zorunlu Mu?                 | Değerler                   | Açıklama                                                |
| ------------------------------- | --------------------------- | -------------------------- | ------------------------------------------------------- |
| <p align="center">`api_key`</p> | <p align="center">evet</p>  | API anahtarı               | API key sahibi olabilmek için lütfen iletişime geçiniz. |
| <p align="center">`il`</p>      | <p align="center">evet</p>  | İl isimleri                |                                                         |
| <p align="center">`ilce`</p>    | <p align="center">hayır</p> | İlde bulunan ilçe isimleri | İlçe parametresi yazılmazsa ildeki tüm nöbetçi eczaneler, yazılırsa ilçedeki nöbetçi eczaneler döndürülür. |

### API Anahtar Seviyeleri ve Aylık Sınırları

| Seviye      | Aylık İstek Sınırı |
| ----------- | ------------------ |
| Bronz       | 100                |
| Gümüş       | 500                |
| Altın       | 1.000              |
| Platin      | 5.000              |
| Elmas       | 10.000             |
| VIP         | Sınırsız           |


![—————————————————————————————————————————————————](./Readme%20Resources/Line.png)

## İstek Örnekleri

İstek örnekleri `curl` komut satırı aracı kullanılarak gösterilmiştir.

✅ **Manisa İli Nöbetçi Eczaneler**

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=manisa"
```

```json
{
  "status": 200,
  "monthly_request_count": 2,
  "result": {
    "city": "Manisa",
    "district": null,
    "districts": [
      "Ahmetli",
      "Akhisar",
      "Alaşehir",
      "Demirci",
      "Gölmarmara",
      "Gördes",
      "Kırkağaç",
      "Köprübaşı",
      "Kula",
      "Salihli",
      "Sarıgöl",
      "Saruhanlı",
      "Şehzadeler",
      "Selendi",
      "Soma",
      "Turgutlu",
      "Yunusemre"
    ],
    "pharmacies": [
      {
        "name": "BORSA ECZANESI",
        "address": "Nısancıpasa Mah. Atatürk Bulvarı No:2/A Hatuniye Cami Karşısı Merkez/Manisa",
        "phone": "0 (236) XXX XX XX",
        "lat": 38.6126,
        "lng": 27.4347
      },
      {
        "name": "İRIER ECZANESI",
        "address": "Hafsa Sultan Mah. Özsaruhan Bulvarı No: 8/B/14 Lale Meydanı-Dürümcü Ali Karşısı Merkez/Manisa",
        "phone": "0 (236) XXX XX XX",
        "lat": 38.6168,
        "lng": 27.4031
      },
      ...
    ]
  },
  "error": null
}
```

✅ **Manisa'nın Akhisar ilçesindeki Nöbetçi Eczaneler**

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=manisa&ilce=akhisar"
```

```json
{
  "status": 200,
  "monthly_request_count": 29,
  "result": {
    "city": "Manisa",
    "district": "akhisar",
    "districts": [
      "Ahmetli",
      "Akhisar",
      "Alaşehir",
      "Demirci",
      "Gölmarmara",
      "Gördes",
      "Kırkağaç",
      "Köprübaşı",
      "Kula",
      "Salihli",
      "Sarıgöl",
      "Saruhanlı",
      "Şehzadeler",
      "Selendi",
      "Soma",
      "Turgutlu",
      "Yunusemre"
    ],
    "pharmacies": [
      {
        "name": "TETIKER ECZANESI",
        "address": "Merkez Çarsı 50 Sok. No:10 Merkez Çarşı-İşbankası Çaprazı Akhisar/Manisa",
        "phone": "0 (236) XXX XX XX",
        "lat": 38.9207,
        "lng": 27.8414
      },
      {
        "name": "SIDAN ECZANESI",
        "address": "Keyhüda Mah. 373 Sok. No:35/A Özel Medigün Hastanesi Acil Kapısı Yanı Akhisar/Manisa",
        "phone": "0 (236) XXX XX XX",
        "lat": 38.928558,
        "lng": 27.835205
      },
      ...
    ]
  },
  "error": null
}
```

✅ **Elazığ Nöbetçi Eczaneler**

Adında Türkçe karakter bulunan il - ilçe fark etmeksizin şehir isimleri olduğu gibi
yada ingilizce karakterlerle yazılabilir ve büyük küçük harf duyarlı değildir.

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=Elazığ"
```

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=elazig"
```

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=ElaZİg"
```

```json
{
  "status": 200,
  "monthly_request_count": 54,
  "result": {
    "city": "Elazığ",
    "district": null,
    "districts": [
      "Ağın",
      "Alacakaya",
      "Arıcak",
      "Baskil",
      "Karakoçan",
      "Keban",
      "Kovancılar",
      "Maden",
      "Merkez",
      "Palu",
      "Sivrice"
    ],
    "pharmacies": [
      {
        "name": "YENI HAYAT ECZANESI",
        "address": "Rızaiye Mah.İnönü Cad.No:70/F (Eski Devlet Hastanesi Karşısı) Vrızaıye Mah. Inönü Cad. No:70/F Merkez/Elazığ",
        "phone": "0 (424) XXX XX XX",
        "lat": 38.6807,
        "lng": 39.2254
      },
      {
        "name": "UFUK ECZANESI",
        "address": "Özel Hayat Hastanesi Karşısı-İzzetpaşa Cami Arkası Vrızaiye Mah. Tatlı Sok. No:4/B Merkez/Elazığ",
        "phone": "0 (424) XXX XX XX",
        "lat": 38.676091,
        "lng": 39.224365
      },
      ...
    ]
  },
  "error": null
}
```

❌ **Yanlış istek**

`il` parametresine geçersiz bir il adı girilirse hata döndürülür.

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=akhisar"
```

```json
{
  "status": 400,
  "monthly_request_count": 104,
  "result": null,
  "error": "Geçersiz il parametresi"
}
```

❌ **Yanlış istek**

`il` ve `ilce` parametreleri uyuşmazsa hata döndürülür.

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=manisa&ilce=simav"
```

```json
{
  "status": 400,
  "monthly_request_count": 7,
  "result": null,
  "error": "Geçersiz ilçe parametresi"
}
```

❌ **Yanlış istek**

Geçerli API key seviyesinin istek sınırına ulaşılmışsa hata döndürülür.

```sh
curl -X GET "https://toktasoft.com/api/duty-pharmacy?api_key=myapikey&il=manisa"
```

```json
{
  "status": 429,
  "monthly_request_count": 10001,
  "result": null,
  "error": "Aylık istek sınırına ulaşıldı"
}
```


![—————————————————————————————————————————————————](./Readme%20Resources/Line.png)

<div align="center">
  <a href="https://github.com/mustafatoktas/W.BE_RepoVisitorCounterAPI"><img src="https://toktasoft.com/api/repo-visitor-counter?repo=7p6kyc5nhzmxru4&show_repo_name=1&show_date=1&show_brand=0&txt_color=209,215,224&bg_color=45,52,58" alt="Repo Visitor Counter"/></a>
</div>

<br>
  
<div align="center">
  <a href="https://buymeacoffee.com/mustafatoktas"><img src="./Readme Resources/Contact/Buy Me a Coffee.png" alt="Buy Me a Coffee" height="64"/></a>
</div>


![—————————————————————————————————————————————————](./Readme%20Resources/Line.png)

## Lisans

```
Copyright 2025 Mustafa TOKTAŞ

Licensed under the GNU General Public License v3.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.gnu.org/licenses/gpl-3.0.html

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```


![—————————————————————————————————————————————————](./Readme%20Resources/Line.png)

## İletişim

<a href="mailto:info@mustafatoktas.com"             ><img src="./Readme Resources/Contact/Mail.png"     alt="Mail"     width="64"/></a>
<a href="https://t.me/mustafatoktas00"              ><img src="./Readme Resources/Contact/Telegram.png" alt="Telegram" width="64"/></a>
<a href="https://www.linkedin.com/in/mustafatoktas/"><img src="./Readme Resources/Contact/LinkedIn.png" alt="LinkedIn" width="64"/></a>

<div align="center">
  <a href="#readme-top"><img src="./Readme Resources/Back to Top.png" alt="Back to Top" height="64"/></a>
</div>
