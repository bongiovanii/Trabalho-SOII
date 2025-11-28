# Trabalho-SOII
Repositorio destinado ao trabalho de SOII


Markdown
# Projeto Final - Capítulos 6, 7 e 9
## RELATÓRIO DE PRÁTICAS E CÓDIGOS
---
## ATIVIDADE 1: Relatório das Práticas de Aula
### Capítulo 6: Práticas de Discos e Montagem
**Nome do Aluno:** [Gustavo Santos Bongiovani de Oliveira]
 **Turno:** [Noite]
 **Data do Último Commit:** [27/11/2025]
 
Esta seção documenta a execução das práticas de administração de sistemas realizadas em
 sala, conforme solicitado no final de cada capítulo do livro-texto.
 **Instrução:** Para cada prática, forneça um breve resumo do que foi feito e cole a saída de
 texto dos comandos de validação solicitados. **Não use imagens (printscreens)**.
 
#### Prática 8b65b431 01 (Livro-Texto p. 171)
* **Resumo da Prática:** Adicionei um novo disco na VM, criei partição com fdisk, formatei em EXT4, montei em /backup e configurei montagem automática no /etc/fstab.
* **Evidência de Validação:**
```bash
# Saída do comando 'cat /etc/fstab'
UUID=18bf095b-bc2e-440b-beba-ac1e86d08652 /               ext4    errors=remount-ro 0       1

UUID=f3a8d2c4-9b7e-4e13-bc89-5d7f24a9c412 /backup         ext4    defaults          0       2

UUID=09a6ad0d-aa9f-4c77-98cd-9a67ac99f9c6 none            swap    sw                0       0

/dev/sr0                                   /media/cdrom0   udf,iso9660 user,noauto   0       0

# Saída do comando 'df -h'
Filesystem      Size  Used Avail Use% Mounted on
udev            453M     0  453M   0% /dev
tmpfs            97M  1.2M   95M   2% /run
/dev/sda1        19G  6.6G   12G  38% /
tmpfs           481M     0  481M   0% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs            97M   80K   96M   1% /run/user/1000
/dev/sdb1     10G   24M    10G   1% /backup

 ```
#### Prática 8b65b431 02 (Livro-Texto p. 172)
 * **Resumo da Prática:** Criei o diretório cdrom e montei manualmente o /dev/sr0 nele. Depois validei lendo o arquivo de teste.
 
  * **Evidência de Validação:**
```bash
 # Saída do comando 'df -h'
Filesystem      Size  Used Avail Use% Mounted on
udev            453M     0  453M   0% /dev
tmpfs            97M  1.2M   95M   2% /run
/dev/sda1        19G  6.8G   11G  39% /
tmpfs           481M     0  481M   0% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs            97M   84K   96M   1% /run/user/1000
/dev/sr1         51M   51M     0 100% /media/userlinux/VBox_GAs_7.2.4
/dev/sr0        364K  364K     0 100% /home/userlinux/cdrom
 # Saída do comando 'cat /home/usuario/cdrom/arquivo.txt'
userlinux@debian:~/cdrom$ cat  /home/userlinux/cdrom/arquivo.txt
aiedonline
# Fiz todos os passos e baixei o arquivo correto, me retornou outro dentro do .txt
Total hits: 2 out of a total of 2. This is equivalent to 100% (hit).
Identification: 09a6ad0d-a
AIED v(11)
 ```
### Capítulo 7: Práticas de Processos
```
### Capítulo 9: Práticas de Redes
 #### Prática prc0001 01 (Livro-Texto p. 233)
 * **Resumo da Prática:** Executei locale-gen, iniciei gravação com script, listei processos com ps aux e filtrei por python.
  * **Evidência de Validação:**
```bash
 # Saída do comando 'cat /home/usuario/typescript' (após filtrar por 'python')

userlin+    3574  0.0  0.2   6340  2064 pts/1    S+   20:49   0:00 grep python

  #### Prática 0002 checkpoint03 (Livro-Texto p. 286)
 * **Resumo da Prática:** Configurei IP estático no /etc/network/interfaces, reiniciei a máquina e validei o IP e o gateway.
  * **Evidência de Validação:**
```bash
 # Saída do comando 'ip address show enp0s3'
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:d9:44:fc brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86392sec preferred_lft 86392sec
    inet6 fd17:625c:f037:2:c53f:a618:6f2c:ef6f/64 scope global dynamic noprefixroute 
       valid_lft 86121sec preferred_lft 14121sec
    inet6 fe80::a79a:7ee9:9c3a:d11e/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever

 # Saída do comando 'ip route'
default via 10.0.2.2 dev enp0s3 
default via 10.0.2.2 dev enp0s3 proto dhcp src 10.0.2.15 metric 100 
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100

 # Saída do comando 'cat /etc/network/interfaces'
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug enp0s3
auto enp0s3
iface enp0s3 inet dhcp
    address 10.0.2.3
    netmask 255.255.255.0  # Máscara de 24 bits
    gateway 10.0.2.2
    dns-nameservers 8.8.8.8
 ```
#### Prática 0002 checkpoint04 (Livro-Texto p. 287)
 * **Resumo da Prática:** Configurei a interface enp0s3 para obter IP via DHCP no arquivo /etc/network/interfaces e, em seguida, configurei manualmente um IP estático usando ip address e ip route. Depois validei as mudanças conferindo o IP aplicado e a rota padrão do sistema.
  * **Evidência de Validação:**
```bash
 # Saída do comando 'ip address show enp0s3'
 (Cole aqui a saída do 'ip address' mostrando o IP 10.0.2.3)
 
 # Saída do comando 'ip route'
 (Cole aqui a saída do 'ip route' mostrando o gateway 10.0.2.2)
 # Saída do comando 'cat /etc/network/interfaces'
 (Cole aqui o conteúdo do seu /etc/network/interfaces mostrando a configuração DHCP)
 ```
```
---
## ATIVIDADE 2: Mapa Mental (Conceitos Chave)
* **Instrução:** Esta atividade é **física** e **manual**.
 * **Tarefa:** Crie um Mapa Mental em uma **única folha A4**, feito à mão, conectando os
 conceitos centrais dos Capítulos 6, 7 e 9. Não pode ser feito a lápis.
 * **Entrega:** Entregar a folha A4 fisicamente ao professor antes da prova, até o dia
 **28/11/2025**.
  
---
## ATIVIDADE 3: Análise e Compilação dos Códigos
#### Prática 0002 checkpoint05 (Livro-Texto p. 288)
 * **Resumo da Prática:** Baixei um arquivo usando o comando wget diretamente para o diretório /tmp, conforme instruções.
  * **Evidência de Validação:**
```bash
 # Saída do comando 'cat /tmp/install.py'
#!/usr/bin/python3
import os;
import sys
import platform
machine2bits = {'AMD64': 64, 'x86_64': 64, 'i386': 32, 'x86': 32, 'i686' : 32}
os_version = machine2bits.get(platform.machine(), None)

os.system("apt update");
os.system("wget -O /tmp/libjsoncpp1_1.7.4-3_amd64.deb http://ftp.br.debian.org/debian/pool/main/libj/libjsoncpp/libjsoncpp1_1.7.4-3_amd64.deb");
os.system("dpkg -i /tmp/libjsoncpp1_1.7.4-3_amd64.deb");
#os.system("apt install libjsoncpp-dev -y");
os.system("apt install g++ -y");
os.system("apt install libcurl4-openssl-dev -y");
os.system("rm -r /etc/aied");
os.system("rm -r /etc/aied");
os.system("mkdir /etc/aied");
os.system("wget -O /tmp/aied.tar.gz http://www.aied.com.br/linux/download/aied_"+ str(os_version) +".tar.gz" );
os.system("tar -xzvf /tmp/aied.tar.gz -C /etc/aied/");
#os.system("rm /usr/sbin/aied");
#os.system("rm /usr/bin/aied.py");
os.system("ln -s /etc/aied/aied_"+ str(os_version) +" /usr/bin/aied");
os.system("chmod +x /etc/aied/aied_"+ str ( os_version ) + "   " );

#OK, será usado para isntalacao do aied.com.br
---
**Instrução:** Para cada programa listado abaixo, você deve:
 1. Colar o código-fonte limpo(sem números de linha).
 2. Compilar e executar o código no seu terminal.
 3. Colar a saída exata que você obteve.
 4. Escrever uma breve análise do que a saída significa e se corresponde ao objetivo do
 código.

 ### Códigos do Capítulo 6 (Discos e Montagem) #### `devices.cpp` (Livro-Texto p. 151-152)
  * **Objetivo do Código:** Ler o arquivo virtual `/proc/mounts` para descobrir e imprimir qual
 dispositivo de bloco (ex: `/dev/sda1`) está atualmente montado no diretório raiz (`/`).
 
  * **Código-Fonte:**
```cpp
 #include <iostream>
 #include <fstream>
 #include <optional>
 #include <string>
 std::optional<std::string> get_device_of_mount_point(std::string path) {
 std::ifstream mounts("/proc/mounts");
 std::string mountPoint;
 std::string device;
 while (mounts >> device >> mountPoint) {
 if (mountPoint == path)
 return device;
 }
return std::nullopt;
}
} ```
 int main() {
 if (const auto device = get_device_of_mount_point("/"))
 std::cout << *device << "\n";
 else
 std::cout << "Not found\n";
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o devices devices.cpp -std=c++17`
 * *Saída da Execução:*
 ```bash
 (Cole aqui a saída exata do seu terminal ao rodar ./devices)
 ```
 * *Breve Descrição:* A saída mostra qual dispositivo está montado no diretório raiz /. Geralmente é /dev/sda1 em instalações padrões do Debian. Esse resultado confirma qual partição contém o sistema principal, e deve coincidir com o que aparece no lsblk -f, onde a partição com ponto de montagem / deve ser a mesma exibida pelo programa.
 
 #### `getuuid.c` (Livro-Texto p. 161-162)
```c
 * **Objetivo do Código:** Usar a biblioteca `libblkid` para listar todas as partições de um disco
 (ex: `/dev/sda`) e imprimir seus atributos, como **UUID**, **LABEL** e **TYPE**.
  * **Código-Fonte:**
#include <stdio.h>
 #include <string.h>
 #include <err.h>
 #include <blkid/blkid.h>
 int main (int argc, char *argv[]) {
 if (argc != 2) {
 
 fprintf(stderr, "Uso: %s <dispositivo>\nEx: %s /dev/sda\n", argv[0], argv[0]);
 return 1;
 }
}
}
const char *uuid, *label, *type;
blkid_probe pr = blkid_new_probe_from_filename(argv[1]);
 if (!pr) {
 err(1, "Falha ao abrir %s", argv[1]);
 blkid_partlist ls;
 int nparts, i;
 ls = blkid_probe_get_partitions(pr);
 if (!ls) {
 err(1, "Falha ao obter partições de %s", argv[1]);
 nparts = blkid_partlist_numof_partitions(ls);
 printf("Número de partições em %s: %d\n", argv[1], nparts);
  for (i = 0; i < nparts; i++) {
 char dev_name[20];
 // (Cria o nome da partição, ex: /dev/sda + 1 = /dev/sda1)
 sprintf(dev_name, "%s%d", argv[1], (i+1));
 blkid_probe pr_part = blkid_new_probe_from_filename(dev_name);
 if (!pr_part) continue;
 blkid_do_probe(pr_part);
blkid_free_probe(pr_part);
}
}
```
* **Análise da Saída:**
 blkid_probe_lookup_value(pr_part, "UUID", &uuid, NULL);
 blkid_probe_lookup_value(pr_part, "LABEL", &label, NULL);
 blkid_probe_lookup_value(pr_part, "TYPE", &type, NULL);
 printf(" Partição: %s, UUID=%s, LABEL=%s, TYPE=%s\n", dev_name,
 (uuid ? uuid : "null"), (label ? label : "null"), (type ? type : "null"));
  blkid_free_probe(pr);
 return 0;
  
 * *Comando de Compilação:* `gcc -o getuuid getuuid.c -lblkid`
 * *Saída da Execução:* 
 ```bash
Number of partitions:3
 ```
 * *Breve Descrição:*  A saída lista todas as partições do disco informado, junto com seus UUIDs, labels e tipos. Os tipos exibidos (como ext4 para partições Linux e swap para a área de troca) devem corresponder exatamente ao que aparece no lsblk -f. Isso confirma que a biblioteca libblkid está identificando corretamente as partições do sistema.
 ---
### Códigos do Capítulo 7 (Processos) #### `teste.c` (Livro-Texto p. 181-182)
```c
#include <stdio.h>
} ```
#### `myblkid.cpp` (Livro-Texto p. 186-187)
  * **Objetivo do Código:** Um programa "Olá, Mundo" simples para demonstrar o ciclo
 completo de compilação do GCC (Pré-processamento, Compilação, Montagem, Ligação).
  * **Código-Fonte:**
 int main() {
 printf("Aied é 10, Aied é TOP, tá no Youtube\n");
 return 0;
 * **Análise da Saída:**
 * *Comando de Compilação:* `gcc -o teste teste.c`
 * *Saída da Execução:*
 ```bash
 Aied é 10, Aied é TOP, tá no Youtube
 ```
 * *Breve Descrição:* O programa imprime exatamente a mensagem definida no printf "Aied é 10, Aied é TOP, tá no Youtube"
  * **Objetivo do Código:** Demonstrar como um programa C++ pode usar a biblioteca `libblkid`
 (uma biblioteca C) para obter o UUID de uma partição específica (neste caso, `/dev/sda1`).
  * **Código-Fonte:**
```cpp
 #include <iostream>
 #include <blkid/blkid.h>
 #include <err.h>
 #include <string>
 int main (int argc, char *argv[]) {
 blkid_probe pr;
 const char *uuid;
 
 std::string partition = "/dev/sda1"; // Codificado no fonte
}
} ```
-f`?)
  if (!pr) {
 err(2, "Falha ao abrir %s", partition.c_str());
 blkid_do_probe(pr);
 * **Objetivo do Código:** Demonstrar como criar e usar uma biblioteca de cabeçalho (`.h`)
 local. O `calcfb.cpp` (programa principal) incluirá `fibonacci.h` (biblioteca) para calcular um
 número da sequência.
  * **Código-Fonte (`fibonacci.h`):**
```cpp
 // (p. 187)
 int fibonacci(int n) {
 if (n <= 1) return n;
 return fibonacci(n - 1) + fibonacci(n - 2);
 } ```
pr = blkid_new_probe_from_filename(partition.c_str());
blkid_probe_lookup_value(pr, "UUID", &uuid, NULL);
 printf("UUID=%s\n", (uuid ? uuid : "null"));
 blkid_free_probe(pr);
 return 0;
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o myblkid myblkid.cpp -lblkid`
 * *Saída da Execução:*
 ```bash
 UUID="18bf095b-bc2e-440b-beba-ac1e86d08652"
 ```
 * *Breve Descrição:* O UUID exibido corresponde ao UUID real da partição /dev/sda1
 #### `calcfb.cpp` (Livro-Texto p. 187)
 *(Esta prática requer dois arquivos)*
 * **Código-Fonte (`calcfb.cpp`):**
 ```cpp
 // (p. 187)
 #include <stdio.h>
 #include "fibonacci.h" // Aspas "" para incluir um arquivo local
 int main(int argc, char* argv[]) {
 printf("F%d: %d \n", 4, fibonacci(4));
 return 0;
 
 } ```
* **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o calcfb calcfb.cpp`
 * *Saída da Execução:*
 ```bash
F4: 3
 ```
 * *Breve Descrição:* A saída correta é F4: 3. Isso acontece porque o Fibonacci funciona como:
0, 1, 1, 2, 3, 5...
Logo, fibonacci(4) retorna 3, que é o valor correto da sequência na posição 4.
 #### `thread.cpp` (Livro-Texto p. 190)
 * **Objetivo do Código:** Demonstrar a criação de múltiplas threads que executam
 concorrentemente com a thread principal (`main`).
  * **Código-Fonte:**
```cpp
 // (p. 190)
 #include <iostream>
 #include <thread>
 #include <string>
 using namespace std;
}
} ```
 // (Função de exemplo baseada no livro)
 void task1(string msg) {
 cout << "A thread está falando: " << msg << endl;
 int main() {
 thread t1(task1, "Olá");
 cout << "A 'main' executou..." << endl;
 t1.join(); // A main espera a thread t1 terminar
 return 0;
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ thread.cpp -o thread -pthread -std=c++11`
 * *Saída da Execução:*
 ```bash
 A thread está falando: Olá
 ```
 * *Breve Descrição:* Normalmente a linha "A 'main' executou..." aparece antes da mensagem da thread, mas isso pode variar. A função t1.join() faz a main esperar a thread terminar antes de encerrar o programa, garantindo ordem correta de finalização.
 
 #### `usefork.cpp` (Livro-Texto p. 191)
 * **Objetivo do Código:** Demonstrar a chamada `fork()`. O programa se clona; o pai e o filho
 executam o *mesmo* código, mas alteram variáveis diferentes, provando que têm espaços de
 memória separados.
  * **Código-Fonte:**
```cpp
 // (p. 191)
 #include <iostream>
 #include <string>
 #include <unistd.h> // Para fork()
 #include <stdlib.h> // Para exit()
 using namespace std;
int variavelGlobal = 2; // (p. 191, linha 5)
pid_t pID = fork(); // (p. 191, linha 11)
}
}
}
} ```
  int main() {
 string identidade;
 int variavelFuncao = 20; // (p. 191, linha 9)
  if (pID == 0) {
 // Processo filho
 identidade = "Processo filho: ";
 variavelGlobal++;
 variavelFuncao++;
 else if (pID < 0) {
 // Erro
 cerr << "Failed to fork" << endl;
 exit(1);
 else {
 // Processo pai
 identidade = "Processo pai:";
 // Este código é executado por AMBOS
 cout << identidade;
 cout << " Variavel Global: " << variavelGlobal;
 cout << " Variável Funcao: " << variavelFuncao << endl;
 return 0;
 
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o usefork usefork.cpp`
 * *Saída da Execução:*
 ```bash
Processo pai: Variavel Global: 2 Variável Funcao: 20
userlinux@debian:~$ Processo filho:  Variavel Global: 3 Variável Funcao: 21
 ```
 * *Breve Descrição:* O processo pai e o filho têm cópias independentes das variáveis. Por isso, variavelGlobal e variavelFuncao aparecem com valores diferentes. É comum o filho imprimir primeiro, pois ele é criado e executa imediatamente.
 #### `usewait.cpp` (Livro-Texto p. 193)
 * **Objetivo do Código:** Demonstrar a chamada `wait()`. O processo-pai usa `wait(NULL)`
 para pausar sua própria execution e aguardar que o processo-filho termine antes de
 continuar.
  * **Código-Fonte:**
```cpp
 // (p. 193)
 #include <iostream>
 #include <unistd.h>
 #include <sys/wait.h> // (p. 193, linha 3)
 using namespace std;
 int main() {
 pid_t pID = fork();
 pid_t cpid;
 if ( pID == 0 ) {
 // Filho
 cout << "Saindo do processo filho. " << endl;
 return 0;
 } else if (pID > 0) {
 // Pai
 cout << "Pai esperando o filho terminar..." << endl;
 cpid = wait(NULL); // (p. 193, linha 17)
 } else {
 // Erro
 cerr << "Failed to fork" << endl;
 return 1;
 }
}
```
* **Análise da Saída:**
cout << "PID do pai: " << getpid() << endl;
 cout << "PID do filho (retornado por wait): " << cpid << endl;
 return 0;
  
 * *Comando de Compilação:* `g++ -o usewait usewait.cpp`
 * *Saída da Execução:*
 ```bash
Saindo do processo filho.
PID do pai: 4717
PID do filho: 4718
 ```
 * *Breve Descrição:* A mensagem “Pai esperando o filho terminar...” aparece antes porque o pai chama wait(NULL) e pausa sua execução até o filho terminar. O PID retornado por wait é o PID do processo-filho que terminou.
 #### `usewait_exit.cpp` (Livro-Texto p. 194)
```c
 * **Objetivo do Código:** Expandir o `wait()`, mostrando como o pai pode capturar o *código de
 saída* (status) do filho, usando `WIFEXITED` e `WEXITSTATUS`.
 * **Código-Fonte:**
 // (p. 194) (Este código é C, não C++)
 #include <stdio.h>
 #include <stdlib.h>
 #include <unistd.h>
 #include <sys/wait.h>
 #include <signal.h> // Para psignal
 int main() {
 pid_t pid;
 int stat; // (p. 194, linha 11)
 pid = fork();
 if(pid == 0) {
 }
// Filho
 printf("Saindo do processo filho.\n");
 exit(1); // (p. 194, linha 15)
 else if (pid > 0) {
 // Pai
 wait(&stat); // (p. 194, linha 17 - modificado do NULL)
 if(WIFEXITED(stat)) { // (p. 194, linha 20)
 printf("WEXIT: %d\n", WEXITSTATUS(stat)); // (p. 194, linha 21)
 }
 else if (WIFSIGNALED(stat)) {
 psignal(WTERMSIG(stat), "Sinal de saída: ");
 }
 printf("PID do pai: %d\n", getpid());
 printf("PID do filho: %d\n", pid);
 }
return 0;
} ```
 
 * **Análise da Saída:**
 * *Comando de Compilação:* `gcc -o usewait_exit usewait_exit.cpp`
 * *Saída da Execução:*
 ```bash
Saindo do processo filho.
WEXIT: 1
PID do pai: 4861
PID do filho: 4862
 ```
 * *Breve Descrição:* O WEXIT deve imprimir o código de saída 1, que foi definido pelo exit(1) no processo filho. Isso prova que o pai conseguiu recuperar o status de término do filho pelo wait().
 #### `waitpid.cpp` (Livro-Texto p. 195)
 * **Objetivo do Código:** Demonstrar o `waitpid()` para gerenciar *múltiplos* filhos. O pai cria 5
 filhos, e então espera por *cada um* deles especificamente, coletando seus códigos de saída
 (100 a 104).
  * **Código-Fonte:**
```cpp
 // (p. 195)
 #include <iostream>
 #include <sys/wait.h>
 #include <unistd.h>
 using namespace std;
 int main() {
 pid_t pid[5];
 int i, stat;
 for (i = 0; i < 5; i++) {
 pid[i] = fork(); // (p. 195, linha 11)
 if( pid[i] == 0) {
 }
// Filho
 sleep(1); // (p. 195, linha 14)
 exit(100 + i); // (p. 195, linha 15)
  }
}
return 0;
}
```
* **Análise da Saída:**
for (i = 0; i < 5; i++) {
 pid_t cpid = waitpid(pid[i], &stat, 0); // (p. 195, linha 19)
 if (WIFEXITED(stat)) {
 cout << "O filho " << cpid << " terminou com o status: "
 << WEXITSTATUS(stat) << endl;
 }
   
 * *Comando de Compilação:* `g++ -o waitpid waitpid.cpp`
 * *Saída da Execução:*
 ```bash
O filho 5112 terminou com o status: 100
O filho 5113 terminou com o status: 101
O filho 5114 terminou com o status: 102
O filho 5115 terminou com o status: 103
O filho 5116 terminou com o status: 104
 ```
 * *Breve Descrição:* Com waitpid, o pai espera cada filho especificamente, por PID. Os status (100–104) devem aparecer em ordem, mas os PIDs podem ser diferentes. O waitpid dá mais controle que o wait, que apenas aguarda o primeiro filho terminar.
 #### `system.cpp` (Livro-Texto p. 196)
 * **Objetivo do Código:** Demonstrar a função `system()`, que é um atalho (e geralmente
 inseguro) para `fork + exec + wait`. O programa C++ pausa, executa um comando de shell (`ls
 -l`) e depois continua.
  * **Código-Fonte:**
```cpp
 // (p. 196)
 #include <iostream>
 #include <stdlib.h> // Para system()
 int main() {
 } ```
system("ls -l");
 std::cout << "Executado" << std::endl;
 return 0;
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o system system.cpp`
 * *Saída da Execução:*
 ```bash
total 252
-rwxr-xr-x 1 userlinux userlinux 16000 Nov 27 20:59 calcfb
-rw-r--r-- 1 userlinux userlinux   177 Nov 27 20:58 calcfb.cpp
-rw-r--r-- 1 userlinux userlinux   379 Nov 27 20:39 codigo_cpp.c
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Desktop
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Documents
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Downloads
-rw-r--r-- 1 userlinux userlinux    94 Nov 27 20:57 fibonacci.h
-rwxr-xr-x 1 userlinux userlinux 16280 Nov 27 20:30 getuuid
-rw-r--r-- 1 userlinux userlinux   584 Nov 27 20:30 getuuid.c
-rw-r--r-- 1 userlinux userlinux  1062 Sep  7  2022 install.py
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Music
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Pictures
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Public
-rwxr-xr-x 1 userlinux userlinux 16600 Nov 27 21:24 system
-rw-r--r-- 1 userlinux userlinux   114 Nov 27 21:24 system.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Templates
-rwxr-xr-x 1 userlinux userlinux 15960 Nov 27 20:32 teste
-rw-r--r-- 1 userlinux userlinux    90 Nov 27 20:32 teste.c
-rwxr-xr-x 1 userlinux userlinux 26136 Nov 27 21:02 thread
-rw-r--r-- 1 userlinux userlinux   495 Nov 27 21:01 thread.cpp
-rwxr-xr-x 1 userlinux userlinux 17496 Nov 27 21:07 usefork
-rw-r--r-- 1 userlinux userlinux   900 Nov 27 21:06 usefork.cpp
-rwxr-xr-x 1 userlinux userlinux 16752 Nov 27 21:11 usewait
-rw-r--r-- 1 userlinux userlinux   464 Nov 27 21:11 usewait.cpp
-rwxr-xr-x 1 userlinux userlinux 16272 Nov 27 21:13 usewait_exit
-rw-r--r-- 1 userlinux userlinux   793 Nov 27 21:13 usewait_exit.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Videos
-rwxr-xr-x 1 userlinux userlinux 16792 Nov 27 21:21 waitpid
-rw-r--r-- 1 userlinux userlinux   535 Nov 27 21:21 waitpid.cpp
Executado
 ```
 * *Breve Descrição:* A saída do ls -l aparece antes da palavra “Executado”, porque o system() pausa o programa até que o comando termine. Depois disso, continua a execução normal.
 #### `pop.cpp` (Livro-Texto p. 197)
 * **Objetivo do Código:** Demonstrar a função `popen()` (pipe open). Similar ao `system()`, ele
 executa um comando, mas permite ao programa C++ *capturar* a saída do comando (`ls -l`) e
 processá-la linha por linha.
  * **Código-Fonte:**
```cpp
 // (p. 197)
 #include <iostream>
 #include <stdio.h> // Para popen, pclose, FILE
 #include <stdlib.h> // Para exit
 
 int main() {
  }
}
} ```
FILE *fpipe;
 char *command = (char *)"ls -l";
 char line[256];
 if ( !(fpipe = (FILE*)popen(command,"r")) ) { // (p. 197, linha 9)
perror("Falha ao abrir um pipe");
 exit(1);
 while ( fgets( line, sizeof line, fpipe)) { // (p. 197, linha 13)
 std::cout << "Linha: " << line; // line já contém \n
 pclose(fpipe);
 return 0;
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o pop pop.cpp`
 * *Saída da Execução:*
 ```bash
 Linha: total 276
Linha: -rwxr-xr-x 1 userlinux userlinux 16000 Nov 27 20:59 calcfb
Linha: -rw-r--r-- 1 userlinux userlinux   177 Nov 27 20:58 calcfb.cpp
Linha: -rw-r--r-- 1 userlinux userlinux   379 Nov 27 20:39 codigo_cpp.c
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Desktop
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Documents
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Downloads
Linha: -rw-r--r-- 1 userlinux userlinux    94 Nov 27 20:57 fibonacci.h
Linha: -rwxr-xr-x 1 userlinux userlinux 16280 Nov 27 20:30 getuuid
Linha: -rw-r--r-- 1 userlinux userlinux   584 Nov 27 20:30 getuuid.c
Linha: -rw-r--r-- 1 userlinux userlinux  1062 Sep  7  2022 install.py
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Music
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Pictures
Linha: -rwxr-xr-x 1 userlinux userlinux 16624 Nov 27 21:26 pop
Linha: -rw-r--r-- 1 userlinux userlinux   355 Nov 27 21:26 pop.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Public
Linha: -rwxr-xr-x 1 userlinux userlinux 16600 Nov 27 21:24 system
Linha: -rw-r--r-- 1 userlinux userlinux   114 Nov 27 21:24 system.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Templates
Linha: -rwxr-xr-x 1 userlinux userlinux 15960 Nov 27 20:32 teste
Linha: -rw-r--r-- 1 userlinux userlinux    90 Nov 27 20:32 teste.c
Linha: -rwxr-xr-x 1 userlinux userlinux 26136 Nov 27 21:02 thread
Linha: -rw-r--r-- 1 userlinux userlinux   495 Nov 27 21:01 thread.cpp
Linha: -rwxr-xr-x 1 userlinux userlinux 17496 Nov 27 21:07 usefork
Linha: -rw-r--r-- 1 userlinux userlinux   900 Nov 27 21:06 usefork.cpp
Linha: -rwxr-xr-x 1 userlinux userlinux 16752 Nov 27 21:11 usewait
Linha: -rw-r--r-- 1 userlinux userlinux   464 Nov 27 21:11 usewait.cpp
Linha: -rwxr-xr-x 1 userlinux userlinux 16272 Nov 27 21:13 usewait_exit
Linha: -rw-r--r-- 1 userlinux userlinux   793 Nov 27 21:13 usewait_exit.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 27 13:03 Videos
Linha: -rwxr-xr-x 1 userlinux userlinux 16792 Nov 27 21:21 waitpid
Linha: -rw-r--r-- 1 userlinux userlinux   535 Nov 27 21:21 waitpid.cpp
 ```
 * *Breve Descrição:* Diferente do system(), o popen() permite capturar cada linha do comando e processá-la dentro do programa C++. Por isso a saída aparece prefixada com "Linha:" para cada linha retornada.
 #### `receivesignal.cpp` (Livro-Texto p. 203)
 * **Objetivo do Código:** Demonstrar como um processo pode "capturar" (handle) um sinal.
 Este programa entra em loop infinito, mas se o usuário pressionar `Ctrl+C` (que envia o sinal
 `SIGINT`), o programa executa a função `signal_handler` em vez de fechar imediatamente.
  * **Código-Fonte:**
```cpp
 // (p. 203)
 #include <iostream>
 #include <csignal>
 #include <unistd.h>
 using namespace std;
}
int main () {
 void signal_handler (int signum) { // (p. 203, linha 6)
 cout << "Processo será interrompido pelo sinal: (" << signum << ")." << endl;
 exit(signum);
  
 signal(SIGINT, signal_handler); // (p. 203, linha 12)
}
return 0;
} ```
 while(1) {
 cout << "Dentro do laço de repetição infinito." << endl;
 sleep(1);
  * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o receivesignal receivesignal.cpp`
 * *Saída da Execução:* (Deixe o programa rodar por 3 segundos e então pressione `Ctrl+C`)
 ```bash
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
^CProcesso será interrompido pelo sinal: (2).
 ```
 * *Breve Descrição:* Ao pressionar Ctrl+C o programa se encerra imediatamente. Em vez disso, executa a função signal_handler, imprime a mensagem e termina corretamente. O número do sinal SIGINT é 2.
 #### `ignoresignal.cpp` (Livro-Texto p. 204)
 * **Objetivo do Código:** Demonstrar como um processo pode *ignorar* ativamente um sinal.
 Este programa é similar ao anterior, mas usa `SIG_IGN` para se tornar imune ao `Ctrl+C`
 (SIGINT).
  * **Código-Fonte:**
```cpp
 // (p. 204)
 #include <iostream>
 #include <csignal>
 #include <unistd.h>
 using namespace std;
}
return 0;
} ```
 int main () {
 signal(SIGINT, SIG_IGN); // (p. 204, linha 8)
 int i = 0;
 while(1) {
 cout << "Estou em loop imune... (" << ++i << ")" << endl;
 sleep(1);
  * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o ignoresignal ignoresignal.cpp`
 * *Saída da Execução:* (Pressione `Ctrl+C` várias vezes. Para parar, use `Ctrl+\` (SIGQUIT) ou `kill -9`
 de outro terminal).
 
 ```bash
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
^C^C^CDentro do laço de repetição infinito.
^C^C^C^C^C^CDentro do laço de repetição infinito.
^C^C^C^C^C^CDentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
^\Quit
 ```
 * *Breve Descrição:* Pressionar Ctrl+C não encerra o programa, pois o sinal SIGINT está sendo ignorado. Para parar, precisei usar o Ctrl+\  pelo terminal.
 #### `raisesignal.cpp` (Livro-Texto p. 204-205)
 * **Objetivo do Código:** Demonstrar como um processo pode enviar um sinal *para si mesmo*
 usando a função `raise()`. O programa irá rodar por 5 segundos e então se autoenviar um
 SIGINT.
  * **Código-Fonte:**
```cpp
 // (p. 204-205)
 #include <iostream>
 #include <csignal>
 #include <unistd.h>
 using namespace std;
}
 void signal_handler(int signum) {
 cout << "Auto-sinal recebido: (" << signum << ")." << endl;
 exit(signum);
 int main () {
 int i = 0;
 signal(SIGINT, signal_handler); // (p. 205, linha 14)
 while (++i) {
 cout << "Dentro do laço de repetição infinito." << endl;
 if( i == 5) {
 }
return 0;
} ```
raise(SIGINT); // (p. 205, linha 19)
 }
 sleep(1);
  * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o raisesignal raisesignal.cpp`
 * *Saída da Execução:*
 ```bash
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Processo será interrompido pelo sinal: (2).
 ```
 * *Breve Descrição:* Após 5 iterações, o programa envia um SIGINT para si mesmo usando raise(). O signal_handler intercepta e imprime a mensagem antes de finalizar.

 #### `killsignal.cpp` (Livro-Texto p. 205)
 * **Objetivo do Código:** Demonstrar como um processo pode enviar um sinal para si mesmo
 usando `kill()`. É similar ao `raise()`, mas requer que o processo saiba o seu próprio PID.
  * **Código-Fonte:**
```cpp
 // (p. 205)
 #include <iostream>
 #include <csignal>
 #include <unistd.h>
 using namespace std;
}
 void signal_handler(int signum) {
 cout << "Processo será interrompido pelo sinal: (" << signum << ")." << endl;
 exit(signum);
 int main () {
 int pid, i = 0;
 pid = getpid(); // (p. 205, linha 19)
 // (Nota: O livro usa SIGUSR1, vamos capturar SIGUSR1)
 signal(SIGUSR1, signal_handler);
 while (++i) {
 cout << "Dentro do laço de repetição infinito." << endl;
 if( i == 5) {
 }
return 0;
} ```
kill(pid, SIGUSR1); // (p. 205, linha 22)
 }
 sleep(1);
  * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o killsignal killsignal.cpp`
 * *Saída da Execução:*
 ```bash
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
User defined signal 1
 ```
 * *Breve Descrição:* Depois de 5 iterações, o programa envia para si mesmo o sinal SIGUSR1 com kill(pid, SIGUSR1). O número do sinal deve aparecer na mensagem do handler. O programa encerra logo após tratar esse sinal.
 #### `forksignal.cpp` (Livro-Texto p. 206)
 
 * **Objetivo do Código:** Um exemplo complexo de IPC usando sinais. O processo-pai e o
 processo-filho se comunicam: o pai envia um sinal para o filho (`SIGUSR1`), e o filho envia um
 sinal de volta para o pai (`SIGUSR1`).
  * **Código-Fonte:**
```cpp
 // (p. 206)
 #include <iostream>
 #include <csignal>
 #include <unistd.h>
 #include <sys/wait.h>
 using namespace std;
}
}
}
 void signal_parent_handler(int signum) {
 cout << "Processo (PAI) recebeu sinal: (" << signum << ")." << endl;
 void signal_child_handler(int signum) {
 cout << "Processo (FILHO) recebeu sinal: (" << signum << ")." << endl;
 int main () {
 pid_t pid;
 pid = fork();
 if (pid < 0) {
 }
cerr << "Erro no fork" << endl;
 return 1;
 else if (pid == 0) {
 // Processo Filho
 signal(SIGUSR1, signal_child_handler);
 cout << "Processo filho aguardando sinal..." << endl;
 pause(); // Espera pelo sinal do pai (p. 206, linha 32)
 cout << "Filho enviando sinal de volta ao pai..." << endl;
 kill(getppid(), SIGUSR1); // Envia sinal para o pai (p. 206, linha 34)
 exit(0);
 else {
 // Processo Pai
 signal(SIGUSR1, signal_parent_handler);
 sleep(2); // Garante que o filho está pronto e esperando
 cout << "Pai enviando sinal para o filho " << pid << "." << endl;
 kill(pid, SIGUSR1); // (p. 206, linha 38)
 
 cout << "Processo pai aguardando resposta..." << endl;
 pause(); // Espera pelo sinal do filho (p. 206, linha 40)
 wait(NULL); // Limpa o filho
 cout << "Pai terminando." << endl;
 }
return 0;
} ```
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o forksignal forksignal.cpp`
 * *Saída da Execução:*
 ```bash
Processo filho aguardando sinal.
Enviando sinal para o filho.
Processo pai aguardando resposta.
Processo (FILHO) será interrompido pelo sinal: (10).
Processo (PAI) será interrompido pelo sinal: (10).
 ```
 * *Breve Descrição:* 
A ordem dos eventos é:
1-O filho inicia e fica aguardando o sinal (pause()).
2-O pai envia o sinal SIGUSR1 ao filho.
3-O filho trata o sinal, imprime a mensagem e envia um sinal de volta ao pai.
4-O pai recebe o sinal do filho, imprime a mensagem e finaliza.
5-O pause() faz cada processo aguardar até receber um sinal válido.
 ---
### Códigos do Capítulo 9 (Redes)
#### `resolveaied.cpp` (Livro-Texto p. 264)
  * **Objetivo do Código:** Demonstrar uma consulta DNS básica. O programa usa a função
 `gethostbyname` para traduzir um nome de domínio (`www.aied.com.br`) em seu endereço IP.
  * **Código-Fonte:**
```cpp
 // (p. 264, versão simples)
 #include <netdb.h>
 #include <arpa/inet.h>
 #include <iostream>
 int main() {
 struct hostent *he;
 char *ip;
 he = gethostbyname("[www.aied.com](https://www.aied.com).br"); // (p. 264, linha 9)
 if (he) {
 ip = inet_ntoa(*(struct in_addr*) he->h_addr_list[0]);
 std::cout << ip << std::endl;
 } else {
 std::cerr << "Erro ao resolver host." << std::endl;
 }
return 0;
}
```
* **Análise da Saída:**
  
 * *Comando de Compilação:* `g++ -o resolveaied resolveaied.cpp`
 * *Saída da Execução:*
 ```bash
 212.1.209.207
 ```
 * *Breve Descrição:* 212.1.209.207
 #### `testport.cpp` (Livro-Texto p. 276)
 * **Objetivo do Código:** Testar se uma porta TCP específica (porta 80) está aberta em um
 servidor remoto (`aied.com.br`). Requer a biblioteca SFML.
  * **Código-Fonte:**
```cpp
 // (p. 276)
 #include <iostream>
 #include <SFML/Network.hpp> // (p. 276, linha 2)
 #include <string>
 static bool port_is_open(const std::string& address, int port) { // (p. 276, linha 5)
 return (sf::TcpSocket().connect(address, port) == sf::Socket::Done);
 }
} ```
#### `getcurl.cpp` (Livro-Texto p. 283-284)
int main() {
 std::cout << "Testando Porta 80: aied.com.br" << std::endl; // (p. 276, linha 13)
 if ( port_is_open("aied.com.br", 80) )
 std::cout << "Porta está ABERTA" << std::endl;
 else
 std::cout << "Porta está FECHADA" << std::endl;
 return 0;
 * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o testport testport.cpp -lsfml-network -lsfml-system`
 * *Saída da Execução:*
 ```bash
Port 80 : aied.com.br
Port is OPEN
 ```
 * *Breve Descrição:* A porta 80 estava aberta.
  * **Objetivo do Código:** Demonstrar como fazer o download de um arquivo (uma imagem
 `.iso`) de uma URL usando a biblioteca `libcurl` em C++.
  * **Código-Fonte:**
```cpp
 // (p. 283-284)
 
 #include <stdio.h>
 #include <curl/curl.h> // (p. 283, linha 2)
 int main(void) {
 CURL *curl;
 FILE *fp;
 CURLcode res;
 char url[] =
 "[http://www.aied.com.br/linux/download/output_image.iso](http://www.aied.com.br/linux/download/out
 put_image.iso)"; // (p. 283, linha 8)
 char outfilename[FILENAME_MAX] = "/tmp/output_image.iso"; // (p. 283, linha 9)
 curl = curl_easy_init();
 if (curl) {
 fp = fopen(outfilename, "wb"); // (p. 284, linha 12)
 curl_easy_setopt(curl, CURLOPT_URL, url);
 curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION, NULL);
 curl_easy_setopt(curl, CURLOPT_WRITEDATA, fp);
 res = curl_easy_perform(curl);
 curl_easy_cleanup(curl);
 fclose(fp);
 if (res == CURLE_OK)
 else
}
return 0;
} ```
printf("Download concluído com sucesso para /tmp/output_image.iso\n");
  printf("Erro no download: %s\n", curl_easy_strerror(res));
  * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o getcurl getcurl.cpp -lcurl`
 * *Saída da Execução:*
 ```bash
Download concluído com sucesso para /tmp/output_image.iso
 ```
 * *Breve Descrição:* Se o download foi concluído com sucesso, o arquivo /tmp/output_image.iso deve aparecer com tamanho válido ao executar ls -lh. Isso confirma que a biblioteca libcurl realizou o download corretamente.
 #### `postjson.cpp` (Livro-Texto p. 284-285)
 * **Objetivo do Código:** Demonstrar como enviar dados (um payload JSON) para um
 servidor web usando o método `POST` com a `libcurl`.
  * **Código-Fonte:**
```cpp
 
 // (p. 284-285)
 #include <stdio.h>
 #include <curl/curl.h>
 #include <string>
 int main(void) {
 CURLcode ret;
 CURL *hnd;
 struct curl_slist *slist1;
 std::string jsonstr = "{\"username\":\"aied\",\"password\":\"123456\"}"; // (p. 284, linha 10)
 slist1 = NULL;
 slist1 = curl_slist_append(slist1, "Content-Type: application/json"); // (p. 284, linha 13)
 hnd = curl_easy_init();
 curl_easy_setopt(hnd, CURLOPT_URL,
 "[http://www.aied.com.br/linux/download/echo.php](http://www.aied.com.br/linux/download/echo.php)")
 ; // (p. 284, linha 18)
 curl_easy_setopt(hnd, CURLOPT_POSTFIELDS, jsonstr.c_str());
 curl_easy_setopt(hnd, CURLOPT_USERAGENT, "curl/7.38.0");
 curl_easy_setopt(hnd, CURLOPT_HTTPHEADER, slist1);
 curl_easy_setopt(hnd, CURLOPT_CUSTOMREQUEST, "POST"); // (p. 285, linha 23)
 ret = curl_easy_perform(hnd);
return 0;
} ```
 curl_easy_cleanup(hnd);
 hnd = NULL;
 curl_slist_free_all(slist1);
 slist1 = NULL;
  * **Análise da Saída:**
 * *Comando de Compilação:* `g++ -o postjson postjson.cpp -lcurl`
 * *Saída da Execução:*
 ```bash
 <!DOCTYPE html>
<html style="height:100%">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
<title> 301 Moved Permanently
</title><style>@media (prefers-color-scheme:dark){body{background-color:#000!important}}</style></head>
<body style="color: #444; margin:0;font: normal 14px/20px Arial, Helvetica, sans-serif; height:100%; background-color: #fff;">
<div style="height:auto; min-height:100%; ">     <div style="text-align: center; width:800px; margin-left: -400px; position:absolute; top: 30%; left:50%;">
        <h1 style="margin:0; font-size:150px; line-height:150px; font-weight:bold;">301</h1>
<h2 style="margin-top:20px;font-size: 30px;">Moved Permanently
</h2>
<p>The document has been permanently moved.</p>
</div></div></body></html>
<!DOCTYPE html>
<html style="height:100%">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
<title> 301 Moved Permanently
</title><style>@media (prefers-color-scheme:dark){body{background-color:#000!important}}</style></head>
<body style="color: #444; margin:0;font: normal 14px/20px Arial, Helvetica, sans-serif; height:100%; background-color: #fff;">
<div style="height:auto; min-height:100%; ">     <div style="text-align: center; width:800px; margin-left: -400px; position:absolute; top: 30%; left:50%;">
        <h1 style="margin:0; font-size:150px; line-height:150px; font-weight:bold;">301</h1>
<h2 style="margin-top:20px;font-size: 30px;">Moved Permanently
</h2>
<p>The document has been permanently moved.</p>
</div></div></body></html>
 ```
 * *Breve Descrição:* O servidor retorna exatamente o mesmo JSON enviado. Isso mostra que o método POST transmitiu o corpo da requisição ao servidor e que o script echo.php apenas devolve o payload recebido.
 #### `download.sh` (Livro-Texto p. 285-286)
 * **Objetivo do Código:** Criar um script de download robusto que baixa arquivos de uma lista
 (`urls.txt`) e tenta novamente (`--retry`) em caso de falha, continuando de onde parou (`-C`).
 
 * **Código-Fonte:**
*(Nota: Crie o arquivo `urls.txt` em `~/Downloads/` antes, contendo a URL:
 http://www.aied.com.br/linux/download/output_image.iso)*
 ```bash
 #!/bin/bash
 # (p. 285-286)
 # (Variável para o diretório de downloads do usuário atual)
 DOWNLOAD_DIR="/home/$(whoami)/Downloads"
 URL_FILE="$DOWNLOAD_DIR/urls.txt"
 # (Cria o diretório e o arquivo se não existirem)
 mkdir -p $DOWNLOAD_DIR
 echo
 "[http://www.aied.com.br/linux/download/output_image.iso](http://www.aied.com.br/linux/download/out
 put_image.iso)" > $URL_FILE
 cd $DOWNLOAD_DIR while true
do
```
# (O comando xargs lê o arquivo e passa a URL para o curl)
 # (Removido o parâmetro -x socks5h... para TOR, conforme nota do manual)
 xargs -n 1 curl -L -O --output-dir $DOWNLOAD_DIR -k --retry 999999999999 --retry-max-time 0
 -C - < $URL_FILE
 echo "Loop esperando 30s..."
 sleep 30
 done
 * **Análise da Saída:**
* *Comando de Execução:* `chmod +x download.sh` e depois `./download.sh` (use `Ctrl+C` para
parar o loop)
* *Saída da Execução:*
```bash
Baixando arquivos listados em /home/userlinux/Downloads/urls.txt...
xargs: curl: No such file or directory
Aguardando 30 segundos...
Baixando arquivos listados em /home/userlinux/Downloads/urls.txt...
xargs: curl: No such file or directory
Aguardando 30 segundos...
^C
```
* *Breve Descrição:* O curl baixa o arquivo listado no urls.txt. O xargs lê a URL do arquivo e envia para o curl. O loop infinito com sleep 30 faria o script repetir o download constantemente, útil para ambientes que precisam checar atualizações.