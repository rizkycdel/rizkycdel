DOKUMENTASI BELAJAR KAFKA ON BASIC

INSTALL JAVA ZOOKEEPER DAN KAFKA PADA SERVER 1: 172.18.46.42
1.	Menginstall Java 
2.	Menjalankan perintah 
cd /etc/yum.repos.d/
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
yum -y install java 
3.	Cek Java yang sudah terinstall dengan perintah
   Java -version

![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/a397666a-0cf0-4c8c-a9bb-e02e676b6752)

4.	Mendownload dan menginstall Kafka dengan perintah
wget https://dlcdn.apache.org/kafka/3.6.1/kafka_2.13-3.6.1.tgz
Mengekstrak file terkompresi dengan perintah 
tar -xvf kafka_2.13-3.0.0.tgz
5.	Menjalankan Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties
 ![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/d0134749-6383-4504-95f9-cb2eabeca4d0)

6.	Setelah Zookeeper Berjalan, Jalankan Kafka Sever dengan perintah
bin/kafka-server-start.sh config/server.properties
 ![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/1b001f73-332b-4ae5-825f-11fb13dee36b)

7.	Membuat Klaster ID dengan perintah
KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"
 ![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/d7c2ef29-9de6-4c87-b2f8-f44954fcd229)

8.	Memformat directory Log dengan perintah
   bin/kafka-storage.sh format -t $KAFKA_CLUSTER_ID -c config/kraft/server.properties –ignore=format
  	
  	 ![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/a70573cc-83fc-49af-930b-5dc7994e1861)

9.	Membuat Topic pada kafka
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
 ![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/723aa7a0-3965-4dfc-8f8f-f3adc4c789c6)

10.	Melihat Topic yang sudah di buat dengan script
    bin/kafka-topics.sh --list --bootstrap-server localhost:9092
 ![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/7b349f41-df4d-46aa-a1c1-ff3e3457302d)

11.	Mengirim Pesan ke Topic
    bin/kafka-console-producer.sh --broker-list localhost:9092 --topic quickstart-alldata
   	![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/0a43febd-ae70-44a2-9537-129a34cb5506)

12.	Meliat Pesan melalui consumer
    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic quickstart-alldata --from-beginning
   	
   	![image](https://github.com/rizkycdel/rizkycdel/assets/154882606/0700a3f0-7bb5-48a3-9816-a74fde638609)

Server 2: 172.18.46.43
// Menginstall JAVA
-cd /etc/yum.repos.d/
-sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
-sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
-yum -y install java
// Install Kafka
wget https://dlcdn.apache.org/kafka/3.6.1/kafka_2.13-3.6.1.tgz
 
// extract file kafka
tar -xzf kafka_2.13-3.6.1.tgz
 

// Menjalankan Zookeeper server
bin/zookeeper-server-start.sh config/zookeeper.properties
 

// Menjalankan Kafka Server
bin/kafka-server-start.sh config/server.properties
 
// Membuat Topic dengan 1 Partitions
bin/kafka-topics.sh --create --topic alldataint --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
 
Output dari Kafka Server
 
// Membuat Topic dengan 2 Partitions
bin/kafka-topic.sh –create --topic contoh-alldataint --bootstrap-server localhost:9092 --partitions 3 –replication-factor 1 
 



// Hasil Output dari Kafka Server
 
// Menampilkan topic yang sudah di create
bin/kafka-topic.sh --list --bootstrap-server localhost:9092
 
// Menginput console producer
bin /kafka-console-producer.sh --broker-list localhost:9092 --topic alldataint  
// Hasil Output dari console-consumer.sh --bootstrap-server localhost:9092 --topic alldataint --from-beginning
NOTE : --from-beginning untuk menampilkan data dari awal di input
 
// Contoh data yang baru di input , akan langsung muncul di console-consumer jika pakai --from-beginning
 

// Contoh console consumer tidak pakai --from-beginning
 

// pengecekan zookeeper quorum dan kafka cluster id
 
 
SERVER 3 : 172.18.46.44
a.	Menginstall Java
 
 

b.	Menginstall Kafka dengan script
wget https://dlcdn.apache.org /kafka/3.6.1/kafka_2.13-3.6.1.tgz
 

Script berikut adalah untuk melihat isi folder/file yang sudah di download dengan proses extract file tersebut
 

Script untuk merubah nama folder agar lebih simple dari nama seblumnya
 

Menjalankan zookeeper server dengan script berikut:
bin/zookeeper-server-start.sh config/zookeeper.properties 
 

Membuka tab baru untuk menjalankan kafka server dengan script berikut:
bin/kafka-server-start.sh config/server.properties
 

Membuka tab baru untuk membuat topic dengan 1 partitions
 


Gambar di bawah adalah hasil dari menjalankan membuat topic dari kafka server
 

Membuat topic dengan 2 partitions
 

Gambar di bawah adalah hasil dari menjalankan perintah di atas
 

Gambar di bawah adalah untuk melihat informasi topic yang sudah di buat 
 

Gambar di bawah adalah untuk melihat informasi topic yang sudah di buat
 
Gambar di bawah adalah contoh untuk membuat atau mengirim pesan pada topic
 

Gambar di bawah adalah hasil untuk melihat apa yang sudah di input pada topic menggunakan fungsi from beginning
 

 

Gambar di bawah adalah hasil untuk melihat topic yang baru di input tanpa menggunakan fungsi from beginning
 


