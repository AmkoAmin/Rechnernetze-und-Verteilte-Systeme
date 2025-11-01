# 🖥️ Rechnernetze und Verteilte Systeme – Praxis Workflow

Dies ist eine kompakte Anleitung zur Bearbeitung, zum Testen und zur Abgabe der Praxis-Aufgaben (Praxis 0, 1, 2) im Modul **Rechnernetze und Verteilte Systeme (EECS, TU Berlin)**.

---

## 📦 1. Projekt-Setup

1. Lade das Skeleton (`praxisX.skeleton.zip`) vom **ISIS-Kurs** herunter.  
2. Entpacke es lokal, z. B. nach:
   ```bash
   mkdir -p ~/rnv && cd ~/rnv
   unzip ~/Downloads/praxisX.skeleton.zip -d praxisX
   ```
3. Bearbeite die Aufgabe im Ordner (z. B. `hello_world.c`, `CMakeLists.txt`).

---

## ⚙️ 2. Lokal kompilieren und testen

### Kompilieren:
```bash
cd ~/rnv/praxisX
cmake -B build && make -C build
./build/hello_world
```

### (Optional) Lokales Testen:
```bash
./test.sh
```

> ⚠️ Achtung:  
> Die Python-Tests funktionieren lokal **nicht zuverlässig**, da sie auf die EECS-Testumgebung (Ubuntu 20, Python 3.8, GCC 9) abgestimmt sind.  
> Für die finale Bewertung müssen die Tests **auf dem TU-Server** bestehen.

---

## ☁️ 3. Projekt auf TU-Server hochladen

> 💡 Stelle sicher, dass du im **TU-VPN** oder im **Eduroam-Netz** bist.

Kopiere dein Projekt mit `scp` auf das TU-Dateisystem:

```bash
scp -r ~/rnv/praxisX/ aminskenderi@sshgate.tu-berlin.de:~/irb-ubuntu/
```

> Dadurch landet dein Projekt im Ordner  
> `/home/tu-berlin.de/aminskenderi/irb-ubuntu/praxisX/`,  
> wo es später auf den Ubuntu 20 EECS-Rechnern getestet wird.

---

## 🔐 4. Verbindung zu den EECS-Servern herstellen

Melde dich per SSH an:

```bash
ssh aminskenderi@ubu20.eecsit.tu-berlin.de
```

Wechsle danach in dein Projekt:

```bash
cd ~/irb-ubuntu/praxisX
```

---

## 🧱 5. Auf dem Server kompilieren

> ❗ Falls du versehentlich den lokalen `build/`-Ordner mitkopiert hast:
> ```bash
> rm -rf build
> ```

Erstelle den Build-Ordner neu und kompiliere dein Programm:
```bash
cmake -B build && make -C build
```

Mit Alias (siehe unten) kannst du auch einfach `cb` schreiben.

---

## 🧪 6. Testen auf dem Server

### Einzelne Tests:
```bash
./test.sh test/test_praxis<X>.py
```

### Alle Tests:
```bash
./test.sh
```

### Offizieller Bewertungs-Testlauf:
```bash
./test/check_submission.sh praxis<X>
```

> ✅ Wenn „1 passed“ erscheint, hast du alles richtig gemacht.

---

## 📦 7. Abgabe erstellen

Erzeuge die Abgabe mit CPack:

```bash
make -C build package_source
```

→ Die Datei befindet sich danach unter:  
`build/RN-Praxis-0.1.1-Source.tar.gz`

Diese `.tar.gz`-Datei musst du auf **ISIS** hochladen.

---

## ⚡ 8. Optional: Alias für schnelles Bauen

Damit du den Build-Befehl kürzer schreiben kannst, füge in deine `~/.bashrc` ein:

```bash
alias cb='cmake -B build && make -C build'
```

Danach kannst du einfach schreiben:
```bash
cb
```

---

## ✅ Zusammenfassung

| Schritt | Befehl |
|----------|--------|
| Projekt hochladen | `scp -r praxisX/ aminskenderi@sshgate.tu-berlin.de:~/irb-ubuntu/` |
| Auf Server verbinden | `ssh aminskenderi@ubu20.eecsit.tu-berlin.de` |
| Kompilieren | `cmake -B build && make -C build` |
| Testen | `./test.sh` oder `./test/check_submission.sh praxis<X>` |
| Abgabe erzeugen | `make -C build package_source` |

---

## 🧠 Hinweise

- Die Tests müssen **auf den Ubuntu 20 EECS-Rechnern** bestehen, nicht lokal.  
- Verwende `rm -rf build` immer, wenn du ein Projekt kopiert hast, um alte Pfade zu löschen.  
- Alle Pfade und Programme auf den Servern sind **case-sensitive** (z. B. `hello_world` ≠ `Hello_World`).  
- Plane vor der Abgabefrist genügend Zeit für Upload und Tests ein.

---

© Technische Universität Berlin · Fachgebiet Telekommunikationsnetze (TKN)
