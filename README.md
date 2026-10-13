# GitHowTo harjutusprojekt "work"

Selles repositooriumis on minu (Markkus Toriland) GitHowTo õpetuse harjutused 2-29, mis tegin
aine **Skriptimisvahendid** raames oma Debian 13 virtuaalmasinas `sv-markkus`.
Projekt ise on väike veebileht (`index.html` + `css/style.css`), aga põhiline eesmärk oli
harjutada Git'i kasutamist käsureal: muudatuste salvestamist, ajalugu, harusid ja konfliktide lahendamist.

Õpetus: [GitHowTo](https://githowto.com/)

## Mida ma selle projekti käigus õppisin

- uue repositooriumi loomine ja esimene commit
- staatuse kontrollimine ning muudatuste lisamine indeksisse (staging)
- commitide tegemine ja ajaloo vaatamine erinevates vormingutes
- vanade versioonide väljavõtmine ja versioonide märgistamine siltidega (tag)
- muudatuste tühistamine enne ja pärast commit'i (`restore`, `revert`, `reset`)
- eelmise commit'i parandamine (`commit --amend`)
- harude loomine, vahetamine ja ühendamine
- failide ümbernimetamine ja liigutamine nii, et Git ajalugu ei kaota
- ühendamiskonflikti tekitamine ja lahendamine
- `merge` ja `rebase` erinevus

## Kasutatud Git'i käsud

### Põhikäsud

| Käsk | Mida teeb |
|------|-----------|
| `git init` | loob kaustas uue repositooriumi |
| `git status` | näitab, mis failid on muudetud, lisatud või jälgimata |
| `git add fail` | lisab muudatuse järgmisesse commit'i |
| `git commit -m "kirjeldus"` | salvestab lisatud muudatused koos kirjeldusega |
| `git log --oneline --graph --all` | näitab ajalugu lühidalt koos harudega |
| `git tag v1` | paneb praegusele commit'ile sildi |

### Harud ja ühendamine

| Käsk | Mida teeb |
|------|-----------|
| `git branch` | näitab olemasolevaid harusid |
| `git switch -c style` | loob uue haru ja liigub sinna |
| `git switch main` | vahetab haru |
| `git merge main` | ühendab teise haru muudatused praegusesse harusse |
| `git rebase main` | tõstab praeguse haru commitid teise haru otsa |

### Muudatuste tagasivõtmine

- `git restore fail` - viskab ära salvestamata muudatused töökaustas
- `git restore --staged fail` - võtab faili indeksist tagasi
- `git revert HEAD` - teeb uue commit'i, mis tühistab eelmise
- `git reset --hard v1` - liigutab haru tagasi valitud versioonile (ettevaatust!)

## Git'i põhitöövoog

Iga muudatuse puhul on töövoog sisuliselt sama:

1. muudan faili töökaustas;
2. kontrollin olukorda käsuga `git status`;
3. lisan muudatuse indeksisse käsuga `git add`;
4. salvestan muudatuse käsuga `git commit`;
5. saadan muudatused GitHubi käsuga `git push`.

Näide ühest tsüklist:

```bash
nano index.html
git status
git add index.html
git commit -m "Lisasin lehele pealkirja"
git push origin main
```

Uue funktsiooni jaoks tasub teha eraldi haru ja see hiljem põhiharuga ühendada:

```bash
git switch -c uus-funktsioon
# ... muudatused, add ja commit ...
git switch main
git merge uus-funktsioon
```

Kui `merge` annab konflikti, tuleb failis märkide `<<<<<<<`, `=======` ja `>>>>>>>` vaheline osa
käsitsi korda teha, seejärel `git add` ja `git commit` (või rebase'i korral `git rebase --continue`).

## Tehtud harjutused

- [x] 2-9: projekti loomine, staging, commitid ja ajalugu
- [x] 10-11: vanad versioonid ja sildid `v1` ning `v1-beta`
- [x] 12-17: muudatuste tühistamine ja commit'i parandamine
- [x] 18-20: haru `style` ning failide liigutamine
- [x] 21-25: harude ühendamine ja konflikti lahendamine
- [x] 26-29: rebase ja `style` haru ühendamine `main` harusse
- [ ] 30+: töö mitme repositooriumiga (järgmine samm)

## Autor

Markkus Toriland - Tartu Rakenduslik Kolledž
