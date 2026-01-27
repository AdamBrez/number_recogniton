# Number Recognition

Projekt pro rozpoznávání ručně psaných číslic pomocí neuronových sítí. Implementace zahrnuje předzpracování dat, trénování MLP modelu a vyhodnocení klasifikační úspěšnosti.

## Struktura projektu

```
├── Main.py                    # Hlavní testovací skript
├── my_main.py                 # Trénování modelu (scikit-learn)
├── architecture.py            # Architektura modelu (PyTorch)
├── MyModel.py                 # Wrapper pro model
├── DataPreprocessing.py       # Předzpracování dat
├── GetScoreOcr.py            # Výpočet F1 skóre
├── data_augmentation.py       # Augmentace dat
├── split_data.py             # Rozdělení dat
├── final_train_data/         # Trénovací data
├── final_val_data/           # Validační data
├── train_dir/                # Trénovací složka
├── val_dir/                  # Validační složka
└── test_dir/                 # Testovací složka
```

## Požadavky

```
numpy
pandas
opencv-python
scikit-learn
torch
torchvision
matplotlib
```

## Instalace

```bash
pip install numpy pandas opencv-python scikit-learn torch torchvision matplotlib
```

## Použití

### Trénování modelu (scikit-learn)

```bash
python my_main.py
```

Skript načte data ze složek train_dir, val_dir a test_dir, provede předzpracování (resize na 28×28, normalizace) a natrénuje MLP klasifikátor s jednou skrytou vrstvou obsahující 128 neuronů.

### Architektura PyTorch

```bash
python architecture.py
```

Struktura modelu:
- Vstupní vrstva: 784 vstupů
- Skrytá vrstva 1: 256 neuronů, ReLU aktivace, Dropout 0.3
- Skrytá vrstva 2: 128 neuronů, ReLU aktivace, Dropout 0.3
- Výstupní vrstva: 10 tříd, Softmax

### Testování modelu

```bash
python Main.py <cesta_k_datum>
```

Skript načte referenční CSV soubor, provede předzpracování vstupních obrázků, klasifikaci pomocí natrénovaného modelu a výpočet F1 skóre s maticí záměn.

## Hlavní komponenty

### DataPreprocessing
Funkce pro předzpracování vstupních obrazových dat. Provádí změnu velikosti, normalizaci a konverzi do požadovaného formátu.

### MyModel
Wrapper funkce pro načtení a aplikaci natrénovaného modelu. Vstupem jsou předzpracovaná data jednoho objektu, výstupem klasifikační třída (0-9).

### GetScoreOcr
Vyhodnocení klasifikační úspěšnosti modelu. Vstupem je matice záměn, výstupem parciální F1 skóre pro jednotlivé třídy a celkové F1 skóre.

## Formát dat

Data jsou organizována do složek podle tříd (zero, one, two, ..., nine). Každá složka obsahuje obrazové soubory příslušné číslice.

Referenční CSV soubor obsahuje sloupce:
- name: název souboru
- target: cílová třída (1-10, kde 10 reprezentuje 0)

## Vyhodnocení

Model je vyhodnocen pomocí:
- Parciální F1 skóre pro každou třídu
- Celkové F1 skóre
- Matice záměn (10×10)

## Datum vytvoření

Říjen 2022
