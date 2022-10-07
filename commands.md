# LINUX - Polecenia i narzędzia do wyświetlenia informacji i szczegółów o urządzeniach i systemie.

## 1. Sprawdzić i wyświetlić informacje o sprzęcie komputerowym w systemach GNU/Linux możemy na dwa sposoby. Za pomocą:

- programów interfejsu graficznego (GUI)
- wiersza poleceń/terminala/konsoli (CLI)

### Konsola/Terminal

Konsola Linuxa jest konsolą systemową zawartą w jądrze Linuxa (kernel).
Pozwalaja na komunikację między użytkownikiem a urządzeniem, za pomocą wydawanych poleceń.
Aktualnie jądro systemu pozwala na wirtualne emulatory konsoli zwane - terminalem, będące oddzielone od jądra, 
a komunikacja odbywa się dzięki powłoce systemowej (shell).
### Jak otworzyć terminal?
W systemie Ubuntu otworzyć terminal możemy za pomocą:
- skrótu klawiszowego `Ctrl + Alt + T`
- klikając prawym przyciskiem myszy na pulpit i wybrać opcję Otwórz terminal
- za pomocą menu z aplikacjami

## 2. Przygotowanie narzędzi
- instalacja pakietu narzędzi `net-tools`:

| Dystrybucja		| Komenda								|
| --- 				| ---									|
| Debian/Ubuntu 	| `sudo apt install net-tools`			|
| Arch/Manjaro		| `sudo pacman -S net-tools`			|
| Fedora			| `sudo dnf install net-tools.x86_64`	|

- instalacja programu `hwinfo`

| Dystrybucja		| Komenda						|
| --- 				| ---							|
| Debian/Ubuntu 	| `sudo apt install hwinfo`		|
| Arch/Manjaro		| `sudo pacman -S hwinfo` 		|
| openSUSE Leap		| `sudo zypper install hwinfo`	|
| Fedora/CentOS 8	| `sudo dnf install hwinfo`		|

- instalacja programu `inxi`

| Dystrybucja		| Komenda					|
| --- 				| ---						|
| Debian/Ubuntu 	| `sudo apt install inxi`	|
| Fedora/CentOS 8	| `sudo dnf install inxi`	|



## 3. Informacje o oprogramowaniu

Jaka jest wersja jądra i czy system jest 64-bitowy oraz jaka jest nazwa hosta, korzystamy z komendy:
```bash
sudo uname -a
```
Aby wyświetlić informacje o UEFI/BIOS skorzystaj z polecenia:
```bash
dmidecode -t bios
```

## 4. Podsumowanie informacji o urządzeniach
### Istnieje kilka poleceń, które pozwalają na pełny przegląd sprzętu komputerowego.

Program `inxi` wylistowuje szczegóły na temat twojego systemu takie jak np.:
- procesor
- grafika
- audio
- sieć
- dyski
- partycje
- czujniki

Aby w pełni wylistować interesujace nas wyżej informacje należy skorzystać z polecenia oraz podanych flag:
```bash
inxi -Fxz
```
Gdzie:
- flaga `-F` oznacza pełne dane wyjściowe
- flaga `-x` dodaje szczegóły
- flaga `-z` ukrywa informacje indentyfikujące jak adresy IP i MAC

Pełne podsumowanie możemy też wyświetlić za pomocą: 
```bash
sudo lshw
```
lub
```bash
sudo hwinfo --short 
```

Jeśli chcemy otrzymać skróconą wersje podsumowania należy dodać flagi dla powyższych poleceń:
```bash
sudo lshw -short 
```
lub dla:
```bash
sudo hwinfo --short 
```

## 5. Procesor
- producent
- model
- częstotliwość

Zobacz szczegóły o procesorze, korzystajac z polecenia `lscpu` lub pokrewnego `lshw`:

```bash
sudo lscpu
```

```bash
sudo lshw -C cpu
```


## 6. Płyta główna
- producent
- model
- wbudowany kontroler

## 7. Pamięci RAM
- rozmiar pamięci
- typ pamięci

```bash
sudo dmidecode -t memory | grep -i size
```

```bash
sudo lshw -short -C memory
```

```bash
sudo dmidecode -t memory | grep -i max
```

```bash
sudo lshw -short -C memory | grep -i empty
```

```bash
sudo hwinfo --memory
```

## 8. Karta graficzna
- model
- producent
- chipset
- pamięć (DRAM, VRAM)
- wielkość pamięci

```bash
sudo lshw -C display
```
```bash
sudo hwinfo --gfxcard
```


## 9. Pamięć masowa
- typ
- producent
- model
- rozmiar
- system magistrali (SCSI, IDE)
- partycjonowanie

```bash
sudo lshw -short -C disk
```

Aby wyświetlić listę wszystkich dysków wraz z wszystkimi ich zdefiniowanymi partycjami, oraz z rozmiarem każdego, skorzystaj z komendy:
```bash
sudo lsblk
```

Do uzyskać większej liczby szczegółów, w tym:
- liczbę sektorów
- rozmiar
- identyfikator i typ systemu plików
- sektory początkowe i końcowe partycji
Warto skorzysatać z:
```bash
sudo fdisk -l
```


```bash
sudo df -m
```

```bash
sudo lsusb
```



## 10. Karta sieciowa

Do wyświetlenia szczegółowych informacji o kartcie sieciowej, skorzystaj z następującej komendy:
```bash
sudo hwinfo --netcard
```

Aby wyświetlić interfejsy sieciowe skorzystaj jednej z komend:
```bash
ifconfig -a
```
lub
```bash
netstat -i
```
lub
```bash
ip link show
```
Przy czytaniu danych wyjściowych pomaga znajomość popularnych skrótów sieciowych:

| Skrót					| Wyjaśnienie								|
| ---					| ---									|
| lo					| Interfejs pętli zwrotnej, tz. localhost	|
| eth0 lub enp*			| Interfejs Ethernet						|
| wlan0					| Interfejs sieci bezprzewodowej		 	|
| ppp0					| Interfejs protokołu Point-to-Point		|
| vboxnet0 lub vmnet*	| Interfejs maszyny wirtualnej				|

Aby wyświetlić bramę domyślną i tabelice routingu, wydaj polecenie:
```bash
netstat -r
```
lub 
```bash
ip route | column -t
```

## 11. Inne dostępne urządzenia:

Urządzenia PCI:
```bash
lspci
```
