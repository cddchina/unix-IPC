# unix-IPC

下载源码，W. Richard Stevens的主页：http://www.kohala.com/start/

wget http://www.kohala.com/start/unpv22e/unpv22e.tar.gz -P /usr/local/src 
2. 解压

tar xvf /usr/local/src/unpv22e.tar.gz -C /root/bin 
3. 编译库文件

cd /root/bin/unpv22e/  
./configure 
编辑生成config.h文件，注释以下几行

vi config.h  
56 // #define uint8_t unsigned char /* <sys/types.h> */  
57 // #define uint16_t unsigned short /* <sys/types.h> */  
58 // #define uint32_t unsigned int /* <sys/types.h> */ 
添加MSG_R和MSG_W定义

vi config.h  
66 // add by jcq  
67 typedef unsigned long ulong_t;  
68 #define MSG_R 0400  
69 #define MSG_W 0200 
添加_GNU_SOURCE定义

vi config.h  
#define _GNU_SOURCE 
编译warpunix.c，使用mkstemp函数替换mktemp函数

cd lib  
181 void  
182 Mktemp(char *template)  
183 {  
184 if (mkstemp(template) == NULL || template[0] == 0)  
185 err_quit("mktemp error");  
186 } 
编译生成libunpipc.a

cd lib  
make 
4. 构建自己的编写代码的目录

mkdir -p /root/bin/unpv2  
cd -  
cp /root/bin/unpv22e/libunpipc.a /root/bin/unpv22e/config.h /root/bin/unpv22e/Make.defines . 


5. 编译各个目录自己的文件

复制各个子目录下得*.h头文件和Makfile文件，然后执行

cp /root/bin/unpv22e/dir/*.h /root/bin/unpv22e/dir/Makefile /root/bin/unpv2
make filename 
即可编译各个子目录下的代码
