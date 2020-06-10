Kubernetes mengoordinasikan sekelompok komputer yang sangat tersedia yang terhubung untuk bekerja sebagai satu unit. Abstraksi di Kubernet memungkinkan Anda untuk menyebarkan aplikasi kemas ke sebuah cluster tanpa mengikatnya secara khusus untuk masing-masing mesin. Untuk menggunakan model penyebaran baru ini, aplikasi perlu dikemas dengan cara yang memisahkan mereka dari host individu: mereka perlu ditampung. Aplikasi kemas lebih fleksibel dan tersedia daripada dalam model penyebaran sebelumnya, di mana aplikasi dipasang langsung ke mesin tertentu sebagai paket terintegrasi ke dalam host. Kubernetes mengotomatiskan distribusi dan penjadwalan wadah aplikasi di seluruh cluster dengan cara yang lebih efisien. Kubernetes adalah platform sumber terbuka dan siap produksi.

Cluster Kubernetes terdiri dari dua jenis sumber daya:

Master mengoordinasi gugus
Node adalah pekerja yang menjalankan aplikasi
Ringkasan:
Cluster Kubernetes
Minikube
Kubernetes adalah platform sumber terbuka dengan tingkat produksi, yang mengatur penempatan (penjadwalan) dan pelaksanaan wadah aplikasi di dalam dan di seluruh kluster komputer.

Master bertanggung jawab untuk mengelola cluster. Master mengoordinasikan semua aktivitas di cluster Anda, seperti menjadwalkan aplikasi, mempertahankan status aplikasi yang diinginkan, menskala aplikasi, dan meluncurkan pembaruan baru.

Node adalah VM atau komputer fisik yang berfungsi sebagai mesin pekerja di kluster Kubernetes. Setiap node memiliki Kubelet, yang merupakan agen untuk mengelola node dan berkomunikasi dengan master Kubernetes. Node juga harus memiliki alat untuk menangani operasi kontainer, seperti Docker atau rkt. Cluster Kubernetes yang menangani lalu lintas produksi harus memiliki minimal tiga node.

Master mengelola cluster dan node yang digunakan untuk meng-host aplikasi yang berjalan.

Saat Anda menggunakan aplikasi di Kubernetes, Anda memberi tahu master untuk memulai wadah aplikasi. Master menjadwalkan kontainer untuk dijalankan pada node cluster. Node berkomunikasi dengan master menggunakan API Kubernetes, yang diekspos master. Pengguna akhir juga dapat menggunakan API Kubernetes secara langsung untuk berinteraksi dengan cluster.

Cluster Kubernetes dapat digunakan pada mesin fisik atau virtual. Untuk memulai pengembangan Kubernetes, Anda bisa menggunakan Minikube. Minikube adalah implementasi Kubernetes ringan yang menciptakan VM pada mesin lokal Anda dan menyebarkan cluster sederhana yang hanya mengandung satu node. Minikube tersedia untuk sistem Linux, macOS, dan Windows. CLI Minikube menyediakan operasi bootstrap dasar untuk bekerja dengan kluster Anda, termasuk mulai, berhenti, status, dan hapus. Namun untuk tutorial ini, Anda akan menggunakan terminal online yang disediakan dengan Minikube yang sudah diinstal sebelumnya.