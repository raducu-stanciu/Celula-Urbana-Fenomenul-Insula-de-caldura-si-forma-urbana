# Data Cards — Analiza Insulei de Căldură Urbană (UHI) în București

**Unitate de analiză spațială:** Grid regulat de 250 m × 250 m (Stereo 70 / EPSG:3844, reproiectat WGS84 / EPSG:4326).  
**Areal:** București și aria periurbană limitrofă (N = 9.009 celule).  
**Fereastră temporală:** Sezonul cald (Iunie – August 2023).

---

## 1. Data Card: USGS Landsat 8/9 Collection 2 Tier 1 Level-2 (LST)

* **Proveniență / Furnizor:** United States Geological Survey (USGS) / NASA via Google Earth Engine (`LANDSAT/LC08/C02/T1_L2`).
* **Perioadă acoperită:** 01.06.2023 – 31.08.2023 (agregare sezonieră prin mediană; filtru nori < 30%).
* **Rezoluție spațială:** Rezoluție nativă termică de 100 m resantionată la 30 m de furnizor; agregată zonal pe celule de 250 m × 250 m.
* **Rezoluție temporală:** Pas de revizitare de 16 zile (8 zile combinat Landsat 8 și Landsat 9).
* **Unități de măsură:** Grade Celsius (°C), calculate prin transformarea radiometrică USGS a benzii termice `ST_B10`:  
  $$\text{LST (°C)} = (\text{DN} \times 0.00341802 + 149.0) - 273.15$$
* **Goluri de date & Tratamente:** Pixeli acoperiți de nori și umbre de nori eliminați utilizând masca de calitate pe biți `QA_PIXEL`. Celulele cu valori nule rezultate din mascare sunt eliminate la filtrarea finală (data attrition).
* **Licență:** Public Domain (USGS open data policy / CC0).

---

## 2. Data Card: Copernicus Sentinel-2 MSI Level-2A (NDVI & NDBI)

* **Proveniență / Furnizor:** Agenția Spațială Europeană (ESA) / Programul Copernicus via Google Earth Engine (`COPERNICUS/S2_SR_HARMONIZED`).
* **Perioadă acoperită:** 01.06.2023 – 31.08.2023 (compozit median sezonier; filtru nori < 25%).
* **Rezoluție spațială:** 10 m (B4 - Red, B8 - NIR), 20 m (B11 - SWIR1); agregată pe celule de 250 m × 250 m.
* **Rezoluție temporală:** 5 zile la ecuator (2–3 zile la latitudinea României prin constelația Sentinel-2A / 2B).
* **Unități de măsură:** Adimensional [-1.0, +1.0]:  
  * $\text{NDVI} = \frac{\text{B8} - \text{B4}}{\text{B8} + \text{B4}}$ (Indicele normalizat de vegetație)  
  * $\text{NDBI} = \frac{\text{B11} - \text{B8}}{\text{B11} + \text{B8}}$ (Indicele normalizat al suprafețelor construite / minerale)
* **Goluri de date & Tratamente:** Mascare pe baza benzii Scene Classification Layer (`SCL`), excluzând clasele de nori, umbră și zăpadă (clasele 3, 8, 9, 10). Agregare mediană zonală.
* **Licență:** Open Access — Copernicus Sentinel Data Terms (utilizare gratuită, academică și comercială).

---

## 3. Data Card: Copernicus Global Human Settlement Layer (GHSL Built-Up)

* **Proveniență / Furnizor:** European Commission Joint Research Centre (JRC) via Google Earth Engine (`JRC/GHSL/P2016/BUILT_LDSMT_GLOBE_V1`).
* **Perioadă acoperită:** Epoci istorice multitemporale de dezvoltare (înregistrare de referință consolidată).
* **Rezoluție spațială:** ~38 m nativ; eșantionat prin puncte centroide pe caroiajul de 250 m × 250 m.
* **Rezoluție temporală:** Static / multianual.
* **Unități de măsură:** Ordinal / Clase categorice discrete [1 – 6]:  
  * `1` = Suprafață de apă  
  * `2` = Teren natural / neconstruit / agricol  
  * `3` = Construit epoca 2000–2014 (dezvoltări periferice recente)  
  * `4` = Construit epoca 1990–2000 (tranziție)  
  * `5` = Construit epoca 1975–1990 (cartiere rezidențiale socialiste)  
  * `6` = Construit anterior anului 1975 (nucleu urban istoric compact)
* **Goluri de date & Tratamente:** Eșantionare la nivel de centroid via `sampleRegions`; valorile neidentificate sunt imputate logic cu clasa 1 (teren deschis/apă).
* **Licență:** Creative Commons Attribution 4.0 International (CC BY 4.0).

---

## 4. Data Card: WorldPop Global High Resolution Population Denominators

* **Proveniență / Furnizor:** WorldPop Research Group (University of Southampton) via Google Earth Engine (`WorldPop/GP/100m/pop`).
* **Perioadă acoperită:** Estimare de referință pentru anul 2020.
* **Rezoluție spațială:** 100 m × 100 m; agregată pe poligoanele gridului de 250 m × 250 m.
* **Rezoluție temporală:** Anual / Proiecție censitară.
* **Unități de măsură:** Număr estimat de rezidenți (persoane per pixel/celulă, scară continuă $\ge 0$).
* **Goluri de date & Tratamente:** Pixeli fără acoperire sau cu densitate nulă sunt imputați cu `0.0` (teren agricol/forestier nelocuit).
* **Licență:** Creative Commons Attribution 4.0 International (CC BY 4.0).