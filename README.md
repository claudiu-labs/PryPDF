Aceasta este documentația tehnică și funcțională a aplicației tale. O poți folosi pentru a explica proiectul unui coleg, unui manager sau pentru a ști tu exact cum funcționează sistemul.

📄 Specificații Tehnice: Aplicație Automatizare Packing List
1. Obiectivul Aplicației
Scopul aplicației este de a elimina munca manuală de modificare a greutăților brute ("Gross Weight") din documentele de tip Delivery Note / Packing List (PDF). Aplicația extrage datele automat, aplică un adaos definit de utilizator și generează un raport final (Excel/PDF).

2. Arhitectura Sistemului
Aplicația este construită pe o arhitectură Web-based Serverless, ceea ce înseamnă că utilizatorul nu trebuie să instaleze nimic pe calculatorul propriu.

Limbaj de programare: Python 3.x

Interfață Utilizator (Frontend): Streamlit

Procesare Date (Backend): Pandas, PDFPlumber, RegEx

Găzduire (Hosting): Streamlit Community Cloud

Stocare Cod (Version Control): GitHub

3. Funcționalități Principale (User Flow)
A. Input (Ce introduce utilizatorul)
Valoarea de Adaos (KG): Un câmp numeric unde utilizatorul specifică greutatea care trebuie adăugată la fiecare tambur (ex: 0.050 KG).

Fișierul Sursă: Posibilitatea de a încărca fișierul PDF original (drag & drop sau browse).

B. Procesare (Ce face "motorul" Python)
Scanare: Scriptul deschide PDF-ul și citește textul de pe toate paginile, indiferent de numărul lor.

Recunoaștere Tipar (Pattern Matching):

Folosește expresii regulate (Regex) pentru a identifica rândurile care conțin date despre tamburi.

Tipar căutat: Cod Tambur (RO...) + Cantitate (...KM) + Gross Weight (...KG) + Net Weight (...KG).

Normalizare Date:

Transformă numerele din format european (ex: 3,988) în format de calcul (ex: 3.988).

Calcul Matematic:

Greutate Brută Nouă = Greutate Brută Originală + Adaos Utilizator.

C. Output (Ce primește utilizatorul)
Previzualizare: Un tabel afișat pe ecran cu primele 5 rânduri procesate, pentru verificare rapidă.

Export Excel (.xlsx): Un fișier Excel formatat, care conține coloanele:

Drum Number

Quantity

Original Gross Weight

New Gross Weight (Valoarea calculată)

Net Weight

4. Detalii Tehnice ale Algoritmului
Expresia Regulată (Regex)
Sistemul nu citește poziții fixe (coordonate X/Y), ci caută structura textului. Asta face aplicația rezistentă la mici decalaje în pagină.

Fragment de cod
(RO\d+)\s+(.+?KM)\s+([\d,.]+\s*KG)\s+([\d,.]+\s*KG)
RO\d+ = Orice cod care începe cu RO urmat de cifre.

.+?KM = Orice text (cantitatea) până la unitatea de măsură KM.

[\d,.]+\s*KG = Greutățile (cifre cu virgulă sau punct) urmate de KG.

Biblioteci Necesare (requirements.txt)
Pentru ca serverul să funcționeze, are nevoie de următoarele pachete instalate:

streamlit (Pentru site)

pdfplumber (Cel mai precis cititor de PDF-uri pentru tabele)

pandas (Pentru manipularea tabelară a datelor)

xlsxwriter (Pentru a scrie fișiere Excel corecte)

5. Structura Fișierelor în GitHub
Pentru ca aplicația să fie "live", repository-ul tău GitHub trebuie să conțină exact aceste două fișiere:

app.py -> Conține tot codul logic (interfața, citirea PDF, calculul).

requirements.txt -> Lista bibliotecilor de mai sus.
