# Terminal

### Rekurzivno nalazi i briše

Prvo nalazi:
```
find . -name "*.spec.js" -type f
```

Potom briše:
```
find . -name "*.spec.js" -type f -delete
```

### Menja ekstenziju

Menja ekstenziju u mala slova:
```
rename 's/\.MD$/.md/' *.MD
```

Menja ekstenziju u mala slova u podfolderima:
```
rename 's/\.MD$/.md/' */*.MD
```

### Menja format slika

Menja image format:
```
convert image.tga image.png
```
Može i masovno:
```
mogrify -format tga *.png  
```
ili
```
for i in *.tga ; do convert "$i" "${i%.*}.png" ; done
```

### Nalazi i menja tekst

Nalazi i menja svaki `tga` sa `png` u fajl.txt:
```
sed -i -- 's/tga/png/g' fajl.txt
```

### Premešta fajlove

Nalazi sve `.mobi` fajlove rekurzivno u podfolderima i premešta ih:
```
find . -name "*.mobi" -exec mv -t literatura/za-citac/ {} +
```

### Preimenuje fajlove

Menja sve nazive fajlova u mala slova:
```
rename 'y/A-Z/a-z/' *
```

### Prikazuje ko zauzima mesto na disku

Prikazuje sve:
```
du -h
```

Prikazuje samo velike potrosace (vise od giga):
```
du -h | grep '[0-9\.]\+G'
```

### Broji fajlove

Prikazuje ukupan broj fajlova:
```
find . -type f | wc -l
```

Prikazuje broj fajlova po direktorijima za trenutni nivo:
```
du -a | cut -d/ -f2 | sort | uniq -c | sort -nr
```

Prikazuje broj fajlova po direktorijima i poddirektorijima:
```
find . -type d -print0 | while read -d '' -r dir; do
    files=("$dir"/*)
    printf "%5d files in directory %s\n" "${#files[@]}" "$dir"
done
```

### Brisanje

Nekad `rm -rf` nece da obrise dir (ako ima nevidljivih i sl). Tada mora:

```
rm -R dir
```

### Razno

Koja sam user grupa:
```
groups $(whoami)
ili
groups $(whoami) | cut -d' ' -f1
```

Štampa čitljiv $PATH:
```
tr : '\n' <<<$PATH
```

Za konzolu u boji, edituj `.bashrc` u home:
```
cd
nano .bashrc
```

Otvara trenutni folder u file exploreru:
```
nautilus .
```

Otvara nezavisno od terminala:
```
nohup (ili)
setsid
```

Proverava apache (apache nece da krene kad se obrise log folder!) :
```
sudo apachectl configtest
```