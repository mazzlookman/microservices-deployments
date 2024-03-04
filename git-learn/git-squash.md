## Git Squash
git-squash adalah:

Contoh kasus:

Current branch: main
Create new branch: fitur-A

Misal kita membuat branch baru (fitur-A) untuk menambah fitur tertentu, di branch fitur-A terdapat >1 commit, <br>

Nah, git squash itu, (branch main) hanya mengambil semua perubahan yang dilakukan oleh branch fitur-A, tanpa melakukan commit apapun. <br>

Dia hanya mengambil semua perubahan oleh fitur-A dan meletakannya di Staging Index, <br> perihal commit itu terserah branch `main`.

Jadi dengan git squash, kita bisa melakukan 1 commit di branch `main` dari semua commit yang dilakukan oleh `fitur-A`.<br>
Sederhananya, menggabungkan banyak commit menjadi 1 commit saja.

Step:

- Buat branch baru, lakukan beberapa perubahan/commit disana.
- Pindah ke branch `main`, kemudian lakukan squash, perintahnya:
 ```shell
git merge --squash nama_branch

# example
git merge --squash fitur-A

# semua perubahan di fitur-A akan ditangkap oleh main
# nah, baru deh lakukan commit

git commit -m "message apa gitu"
```
