# Tahák `pandas`
  
## Import pandas
```py
import pandas as pd
```

## Vytvoření prázdného DataFrame
```py
prazdny_dataframe = pd.DataFrame()
dataframe_se_sloupecky = pd.DataFrame(columns=["sloupec1", "sloupec2", "sloupec3"])
```

## Načítání dat
Data můžeš načítat z různých souborů (CSV, Excel, JSON atd.):
```py
novy_dataframe = pd.read_csv("nazev_souboru.csv")
json_dataframe = pd.read_json("nazev_souboru.json")
excel_dataframe = pd.read_excel("nazev_souboru.xlsx", sheet_name="list1")
```

### Další parametry při načítání CSV
```py
novy_dataframe = pd.read_csv("nazev_souboru.csv", sep=";")
```
- `sep=";"` – pro soubory oddělené středníkem

## Index
```py
muj_dataframe.set_index("sloupecek", inplace=True) # nastaví nový index
muj_dataframe.reset_index(inplace=True) # resetuje index zpět na implicitní
```

## Základní informace o tabulce
```py
muj_dataframe.info() # základní informace o DataFrame (sloupce, typy, chybějící data)
muj_dataframe.shape # (počet řádků, počet sloupců)
muj_dataframe.columns # názvy všech sloupců
muj_dataframe.describe(include="all") # souhrnné statistiky včetně kategorií

muj_dataframe.head(10) # prvních 10 řádků
muj_dataframe.tail(3) # poslední 3 řádky
muj_dataframe.sample(5) # 5 náhodných řádků
```

## Výběr sloupců
```py
muj_dataframe["Nazev sloupce"] # vrací Series (jednosloupcová struktura)
muj_dataframe[["Nazev sloupce", "Dalsi nazev sloupce"]] # vrací DataFrame (vícesloupcová struktura)
```

## Výběr řádků pomocí indexu
```py
muj_dataframe.iloc[1:10]    # řádky 1 až 9 (0-based indexování)
muj_dataframe.iloc[:3]      # první tři řádky
muj_dataframe.iloc[-3:]     # poslední tři řádky
muj_dataframe.iloc[8:]      # od osmé řádky dále
```

## Výběr řádků i sloupců
```py
muj_dataframe.iloc[:, [0, 3]] # všechny řádky a pouze sloupce 0 a 3
muj_dataframe.loc[1:4, ["Nazev Sloupce"]] # vybraný rozsah řádků a sloupce podle názvu
```

## Filtrování dat
```py
filtrovany_dataframe = muj_dataframe[muj_dataframe["Nazev sloupce"] > 100] # podmíněný výběr
filtrovany_dataframe = muj_dataframe[(muj_dataframe["sloupec1"] > 50) & (muj_dataframe["sloupec2"] == "hodnota")] 
```

## Spojování dat (UNION)
```py
# Svislé spojení (appendování řádků)
svisle_slouceni = pd.concat([df1, df2], axis=0)

# Vodorovné spojení (spojení sloupců)
vodorovne_slouceni = pd.concat([df1, df2], axis=1)
```

## Spojování dat (JOIN)
```py
# Levé spojení (left join) podle společného sloupce
slouceny_dataframe = pd.merge(df1, df2, on="spolecny_sloupec", how="left")

# Pravé spojení (right join)
slouceny_dataframe = pd.merge(df1, df2, on="spolecny_sloupec", how="right")

# Vnitřní spojení (inner join)
slouceny_dataframe = pd.merge(df1, df2, on="spolecny_sloupec", how="inner")

# Vnější spojení (outer join)
slouceny_dataframe = pd.merge(df1, df2, on="spolecny_sloupec", how="outer")
```

## Skupinové operace a agregace
```py
muj_dataframe.groupby("Nazev sloupce").mean() # průměrné hodnoty pro každou skupinu
muj_dataframe.groupby("Nazev sloupce")["jiny_sloupec"].sum() # suma v jiném sloupci podle skupin
```

## Agregace pomocí `agg()`
```py
# Použití různých agregací pro různé sloupce
agregovany_dataframe = muj_dataframe.groupby("Nazev_skupiny").agg({
    "sloupec1": "sum", 
    "sloupec2": ["min", "max"],
    "sloupec3": "mean"
})
```

## Práce s chybějícími hodnotami
```py
muj_dataframe.isna().sum() # počet chybějících hodnot v každém sloupci
muj_dataframe.fillna(0) # nahradí chybějící hodnoty nulami
muj_dataframe.dropna() # odstraní všechny řádky s chybějícími hodnotami
```

## Pivot tabulka
```py
# Vytvoření pivot tabulky
kontingencni_tabulka = pd.pivot_table(muj_dataframe, values="hodnota", index="index_sloupec", columns="sloupec", aggfunc="sum")
```

## Crosstab (Kontingenční tabulka)
```py
# Crosstab mezi dvěma kategoriemi
kontingencni_tabulka = pd.crosstab(muj_dataframe["sloupec1"], muj_dataframe["sloupec2"])
```
