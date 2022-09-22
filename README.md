# Osintgram
Instagram About


# Osintgram 🔎📸

[![version-1.3](https://img.shields.io/badge/version-1.3-green)](https://github.com/Datalux/Osintgram/releases/tag/1.3)
[![GPLv3](https://img.shields.io/badge/license-GPLv3-blue)](https://img.shields.io/badge/license-GPLv3-blue)
[![Python3](https://img.shields.io/badge/language-Python3-red)](https://img.shields.io/badge/language-Python3-red)
[![Telegram](https://img.shields.io/badge/Telegram-Channel-blue.svg)](https://t.me/osintgram)
[![Docker](https://img.shields.io/badge/Docker-Supported-blue)](https://img.shields.io/badge/Docker-Supported-blue)

Osintgram adalah alat **OSINT** di Instagram untuk mengumpulkan, menganalisis, dan menjalankan pengintaian.



Disclaimer: **KHUSUS UNTUK TUJUAN PENDIDIKAN! Kontributor tidak bertanggung jawab atas penggunaan alat ini.**

Peringatan: Disarankan untuk **tidak** menggunakan akun Anda sendiri/utama saat menggunakan alat ini.

## Tools and Commands 🧰

Osintgram menawarkan shell interaktif untuk melakukan analisis pada akun Instagram setiap pengguna dengan nama panggilannya. Kamu bisa mendapatkan:

```text
- addrs           Dapatkan semua alamat terdaftar dengan foto target
- captions        Dapatkan keterangan foto pengguna
- comments        Dapatkan total komentar dari posting target
- followers       Dapatkan target pengikut
- followings      Dapatkan pengguna diikuti oleh target
- fwersemail      Dapatkan email pengikut target
- fwingsemail     Dapatkan email pengguna diikuti oleh target
- fwersnumber     Dapatkan nomor telepon pengikut target
- fwingsnumber    Dapatkan nomor telepon pengguna diikuti oleh target
- hashtags        Dapatkan hashtag yang digunakan oleh target
- info            Dapatkan info sasaran
- likes           Dapatkan total suka dari posting target
- mediatype       Dapatkan jenis posting pengguna (foto atau video)
- photodes        Dapatkan deskripsi foto target
- photos          Unduh foto pengguna di folder keluaran
- propic          Unduh gambar profil pengguna
- stories         Unduh cerita pengguna
- tagged          Dapatkan daftar pengguna yang ditandai berdasarkan target
- wcommented      Dapatkan daftar pengguna yang mengomentari foto target
- wtagged         Dapatkan daftar pengguna yang menandai target
```

Anda dapat menemukan penggunaan perintah terperinci [di sini](doc/COMMANDS.md).

[**Versi terbaru**](https://github.com/Datalux/Osintgram/releases/tag/1.3) |
[Perintah](doc/COMMANDS.md) |
[CHANGELOG](doc/CHANGELOG.md)

## FAQ
1. **Dapatkah saya mengakses konten profil pribadi?** Tidak, Anda tidak dapat memperoleh informasi tentang profil pribadi. Anda hanya bisa mendapatkan informasi dari profil publik atau profil yang Anda ikuti. Alat yang mengklaim berhasil adalah penipuan!
2. **Apa itu dan bagaimana saya bisa melewati kesalahan `challenge_required`?** Kesalahan `challenge_required` berarti bahwa Instagram melihat perilaku mencurigakan di profil Anda, jadi perlu memeriksa apakah Anda orang sungguhan atau bot. Untuk menghindari ini, Anda harus mengikuti tautan yang disarankan dan menyelesaikan operasi yang diperlukan (masukkan kode, konfirmasi email, dll)


## Installation ⚙️

1. Fork/Clone/Download this repo

    `git clone https://github.com/Datalux/Osintgram.git`

2. Navigate to the directory

    `cd Osintgram`

3. Create a virtual environment for this project

    `python3 -m venv venv`

4. Load the virtual environment
   - On Windows Powershell: `.\venv\Scripts\activate.ps1`
   - On Linux and Git Bash: `source venv/bin/activate`
  
5. Run `pip install -r requirements.txt`

6. Open the `credentials.ini` file in the `config` folder and write your Instagram account username and password in the corresponding fields
    
    Alternatively, you can run the `make setup` command to populate this file for you.

7. Run the main.py script in one of two ways

    * As an interactive prompt `python3 main.py <target username>`
    * Or execute your command straight away `python3 main.py <target username> --command <command>`
    
### Use Osintgram v2 (beta)
You can use Osintgram2 beta just switching to `v2` [branch](https://github.com/Datalux/Osintgram/tree/v2).
The v2 has some improvements and faster with a new command execution interface. Try it just running `git checkout v2`.

## Docker Quick Start 🐳

This section will explain how you can quickly use this image with `Docker` or `Docker-compose`.

### Prerequisites

Before you can use either `Docker` or `Docker-compose`, please ensure you do have the following prerequisites met.

1. **Docker** installed - [link](https://docs.docker.com/get-docker/)
2. **Docker-composed** installed (if using Docker-compose) - [link](https://docs.docker.com/compose/install/)
3. **Credentials** configured - This can be done manually or by running the `make setup` command from the root of this repo

**Important**: Your container will fail if you do not do step #3 and configure your credentials

### Docker

If docker is installed you can build an image and run this as a container.

Build:

```bash
docker build -t osintgram .
```

Run:

```bash
docker run --rm -it -v "$PWD/output:/home/osintgram/output" osintgram <target>
```

- The `<target>` is the Instagram account you wish to use as your target for recon.
- The required `-i` flag enables an interactive terminal to use commands within the container. [docs](https://docs.docker.com/engine/reference/commandline/run/#assign-name-and-allocate-pseudo-tty---name--it)
- The required `-v` flag mounts a volume between your local filesystem and the container to save to the `./output/` folder. [docs](https://docs.docker.com/engine/reference/commandline/run/#mount-volume--v---read-only)
- The optional `--rm` flag removes the container filesystem on completion to prevent cruft build-up. [docs](https://docs.docker.com/engine/reference/run/#clean-up---rm)
- The optional `-t` flag allocates a pseudo-TTY which allows colored output. [docs](https://docs.docker.com/engine/reference/run/#foreground)

### Using `docker-compose`

You can use the `docker-compose.yml` file this single command:

```bash
docker-compose run osintgram <target>
```

Where `target` is the Instagram target for recon.

Alternatively you may run `docker-compose` with the `Makefile`:

`make run` - Builds and Runs with compose. Prompts for a `target` before running.

### Makefile (easy mode)

For ease of use with Docker-compose, a `Makefile` has been provided.

Here is a sample work flow to spin up a container and run `osintgram` with just two commands!

1. `make setup`   - Sets up your Instagram credentials
2. `make run`     - Builds and Runs a osintgram container and prompts for a target

Sample workflow for development:

1. `make setup`          - Sets up your Instagram credentials
2. `make build-run-testing`   - Builds an Runs a container without invoking the `main.py` script. Useful for an `it` Docker session for development
3. `make cleanup-testing`     - Cleans up the testing container created from `build-run-testing`

## Development version 💻

To use the development version with the latest feature and fixes just switch to `development` branch using Git:

`git checkout development`

and update to last version using:

`git pull origin development`


## Updating ⬇️

Untuk memperbarui Osintgram dengan rilis stabil, cukup tarik komit terbaru menggunakan Git.

1. Make sure you are in the master branch running: `git checkout master`
2. Download the latest version: `git pull origin master`



[Instagram API](https://github.com/ping/instagram_private_api)
