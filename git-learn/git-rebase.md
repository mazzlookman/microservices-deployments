### Git Rebase
git rebase adalah:

- merupakan cara lain melakukan merge
- bedanya ini lebih rapih, karena timeline-nya hanya 1 timeline
- tidak membuat commit baru (kalo merge kan membuat commit baru dengan message default)
- tapi ini menulis ulang semua commit yang dilakukan, sehingga commit id sebelum2nya dan jika ada tag maka akan hilang. 

Contoh kasus:

Current branch: main
Create new branch: fitur-A

Misal kita membuat branch baru (fitur-A) untuk menambah fitur tertentu, di branch fitur-A terdapat >= 1 commit, <br>

Nah git-rebase itu menarik branch main kedalam fitur-A, posisi commit terakhir main tetap dibelakang, yang di HEAD-nya itu commit-an fitur-A
Sederhananya, kita hanya menarik semua commit di main ke fitur-A, itu aja. Perihal commit-an posisinya tetap.

Perintah:
```shell
# current branch: fitur-A
git rebase main
```

Kemudian agar posisi main sama dengan fitur-A (di HEAD), lakukan merge. Perintahnya:
```shell
# pindah ke main dulu
git checkout main

# lakukan merge (hanya melakukan fast-forward main ke HEAD)
git merge main

# sudah deh selese
```





