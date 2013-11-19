#include <stdio.h>
struct clientes
{
int nip;
long int ncuenta;
char nombre [10];
long int saldo;
char direccion[10];
};
FILE *parchivo;
int cambiar (int i,int A);
void leeropcion(int *opc);
void menu ();
void resta(struct clientes *c,int pos,int entero);
void escribir(struct clientes *c,int pos);
void suma(struct clientes *c,int pos,int entero);
void guardarArchivo(struct clientes);
int main(int argc, char* argv[])
 
{
/* Declaracion de variables*/
char marc;
int W,cantidad,op,mont,ret,num,i,T,N,S,sobregiro;
struct clientes clientes[5];
struct clientes *p;
p=clientes;
printf ("Cuantas cuentas desea ingresar?\n");
scanf ("%d",&num);
for (i=0;i<num;i++)
{
printf ("Ingresa nip %d:",i+1);
scanf ("\n%d%*c",&(p+i)->nip);
printf ("Ingresa numero de cuenta %d:",i+1);
scanf("\n%ld%*c",&(p+i)->ncuenta);
printf ("Ingresa saldo de la cuenta %d: ",i+1);
scanf ("\n%ld%*c",&(p+i)->saldo);
printf ("Ingresael nombre del usuario %d:",i+1);
gets((p+i)->nombre);
printf ("Ingresala direccion del usuario %d:",i+1);
gets ((p+i)->direccion);
/* escribir datos en archivo */
if((parchivo = fopen("datos.dat", "wb"))==NULL)
{printf("No se puede abrir el archivo\n");
exit(0);}
fwrite(clientes,sizeof(clientes),1,parchivo);
fclose(parchivo);
}
/* lectura de datos en archivo y mostrarlos en pantalla*/
if ((parchivo = fopen(argv[1],"rb")) == NULL)
{
printf ("Error en apertura del fichero para lectura \n" );
}
else
{ fread(clientes,sizeof(clientes),1,parchivo);
printf("No. Cuenta\tNip\tSaldo\tNombre\tDireccion\n");
for (i=0;i<num;i++)
{
 
printf ("%ld\t\t",(p+i)->ncuenta);
printf ("%d\t",(p+i)->nip);
printf ("%ld\t",(p+i)->saldo);
printf ("%s\t",(p+i)->nombre);
printf ("%s\t",(p+i)->direccion);
printf ("\n");
fread(clientes,sizeof(clientes),1,parchivo);
}
fclose (parchivo);
}
 
printf ("Escriba numero de cuenta a la que quiere retirar\n");
scanf ("%d",&T);
for (i=0;i<num;i++)
if ((p+i)->ncuenta==T)
T=cambiar(i,T);
do
{
printf("░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░\n");
printf("░ ░\n");
printf("░ ░\n");
printf("░ Cajero Automático ░\n");
printf("░ ░\n");
printf("░ ░\n");
printf("░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░\n");
menu();
leeropcion(&op);
if (op<1 || op>7)
printf("Opcion no valida\n");
else
{
switch(op)
 
/*Empieza switch principal*/
{
case 1:
/*Empieza caso 1*/
 
 
 
 
{
if ((p+T)->saldo>0)
{
printf("SELECCIONE EL MONTO\n");
printf("1)-$50\n");
printf("2)-$100\n");
printf("3)-$200\n");
printf("4)-$500\n");
printf("5)-$1000\n");
printf("6)-$1500\n");
printf("7)-$2000\n");
printf("8)Otra cantidad\n");
scanf("%d",&mont);
if(mont<1 || mont>8) printf("Opcion no valida\n");
else
{
 
 
switch(mont)
/*Empieza switch mont*/
{
 
case 1:
/*Empieza case 1.1*/
{
cantidad=50;
if ((p+T)->saldo>cantidad)
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
}
 
else
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
}
break;
}
/*termina case 1.1*/
 
case 2:
/*inicia case 2*/
{
cantidad=100;
if ((p+T)->saldo>=cantidad)
/*comparando*/
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
}
else
{
resta (p,T,cantidad);
sobregiro=((p+T)->saldo-cantidad)*(-1);
printf("Su transaccion esta siendo procesada...\n");
printf("Tienes un sobregiro de $%d\n\n",sobregiro);
 
}
break;
}
/*termina case 2*/
case 3:
/*empieza case 3*/
{
cantidad=200;
if ((p+T)->saldo>=cantidad)
/*comparando*/
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
}
else
{
resta (p,T,cantidad);
sobregiro=((p+T)->saldo-cantidad)*(-1);
printf("Su transaccion esta siendo procesada...\n");
printf("Tienes un sobregiro de $%d\n\n",sobregiro);
}
break;
}
/*termina case 3*/
 
case 4:
/*empieza case 4*/
{
cantidad=500;
if (p->saldo>=cantidad)
/*comparando*/
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
}
else
printf ("cuenta sin fondos");
break;
 
}
/*termina case 4*/
 
case 5:
/*empieza case 5*/
{
cantidad=1000;
if ((p+T)->saldo>=cantidad)
/*comparando*/
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
}
else
printf ("cuenta sin fondos");
break;
}
/*termina case 5*/
case 6:
/*Comienza case 6*/
{
cantidad=1500;
if ((p+T)->saldo>=cantidad)
/*comparando*/
{
resta (p,T,cantidad);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
 
}
else
printf ("cuenta sin fondos");
break;
}
/*termina case 6*/
 
case 7:
/*empieza case 7*/
{
if (p->saldo>=2000)
/*comparando*/
{
resta (p,T,2000);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
 
}
else
printf ("cuenta sin fondos");
break;
}
/*termina case 7*/
 
case 8:
/*empieza case 8*/
 
{
printf("Digita la cantidad a retirar\n");
scanf("%d",&ret);
if ((p+T)->saldo>=ret)
/*comparando*/
{
resta (p,T,ret);
printf("Su transaccion esta siendo procesada...\n");
printf("Su monto actual es $%ld\n\n",(p+T)->saldo);
 
}
else
printf ("cuenta sin fondos");
break;
}
/*termina case 8*/
 
 
 
 
/*Termina switch mont*/
}
/*termina else*/
}
 
}
else
printf ("Operacion no valida\n");
break;
}
/*Termina caso 1*/
 
case 2:
 
 
/*empieza case 2 principal*/
{
if ((p+T)->saldo>0)
escribir (p,T);
 
else
printf ("Su saldo es deudor\n");
 
break;
 
}
/*termina case 2 principal*/
case 3:
/*empieza case 3 principal*/
{
if ((p+T)->saldo>0)
{
printf ("Digite el numero de cuenta a la cual le quiere hacer el deposito\n");
scanf ("%d",&W);
 
printf("Digite el importe de traspaso maximo:%ld\n\n",(p+T)->saldo);
scanf("%d",&cantidad);
if ((p+T)->saldo>=cantidad)
{
for (i=0;i<num;i++)
if ((p+i)->ncuenta==W)
S=cambiar( i,W);
if ((p+S)->ncuenta==W){
printf ("Usted va a realizar un transpaso a la cuenta:%d",W);
printf ("por el monto $%d\n\n\n",cantidad);
resta (p,T,cantidad);
suma (p,S,cantidad);
}
else{
printf("Usted va a realizar un traspaso a la cuenta:%d\n",W);
printf("Por el monto $%d\n\n\n",cantidad);
resta (p,T,cantidad);
}
}
else
printf ("El importe debe ser maximo de %ld\n\n\n",(p+T)->saldo);
}
else
printf ("cuenta sin fondos");
break;
}
/*termina case 3 principal*/
 
 
case 4:
/*empieza case 4 principal*/
{
if ((p+T)->saldo>0){
printf("Seleccione marca del producto\n");
printf("T)-TELCEL\nM)-MOVISTAR\n");
scanf("%s",&marc);
switch(toupper(marc))
/*primer switch para elegir marca*/
{
case 'T':
{
printf("Seleccione importe deseado de tarjeta de amigo Telcel\n");
printf("$50\n");
printf("$100\n");
printf("$200\n");
printf("$300\n");
printf("$500\n");
scanf("%d",&mont);
switch(mont)
{
case 50:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,50);
break;
}
case 100:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,100);
break;
}
case 200:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,200);
break;
}
 
case 300:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,300);
 
break;
}
 
case 500:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,500);
break;
}
 
}
/*switch mont termina*/
printf("Usted ha seleccionado un(a) tarjeta amigo de telcel con un valor de $%d\n",mont);
printf("El servicio solicitado sera abonado automaticamente al numero (044)-%d\n\n\n",N);
}
/*termina case T*/
break;
case 'M':
{
printf("Seleccione importe deseado\n");
printf("$50\n");
printf("$100\n");
printf("$200\n");
printf("$300\n");
printf("$500\n");
scanf("%d",&mont);
switch(mont)
{
case 50:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,50);
}
break;
case 100:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,100);
}
break;
case 200:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,200);
}
break;
case 300:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,300);
}
break;
case 500:
{
printf("Digite el numero al que desea abonar\n");
scanf("%d",&N);
resta (p,T,500);
}
break;
}
/*switch mont para M termina*/
printf("Usted ha seleccionado un(a) tarjeta amigo de telcel con un valor de $%d\n",mont);
printf("El servicio solicitado sera abonado automaticamente al numero (044)-%d\n\n\n",N);
 
}
/*termina case M*/
break;
 
}
/*termina switch marca*/
 
 
}else
printf ("Operacion no valida\n");
}
/*termina case 4 principal*/
break;
/*inicia case 0 principal*/
case 5:
{
printf ("Escriba su numero de cuenta\n");
scanf ("%d",&T);
for (i=0;i<num;i++)
if (T==(p+i)->ncuenta)
T=cambiar(i,T);
break;
}
case 6:
{
for (i=0;i<num;i++)
{
if((parchivo = fopen("datos.dat", "wb"))==NULL)
{printf("No se puede abrir el archivo\n");
exit(0);}
fwrite(clientes,sizeof(clientes),1,parchivo);
fclose(parchivo);
}
break;
}
case 7:
{
if ((parchivo = fopen(argv[1],"rb")) == NULL)
{
printf ("Error en apertura del fichero para lectura \n" );
}
else
{ fread(clientes,sizeof(clientes),1,parchivo);
printf("No. Cuenta\tNip\tSaldo\tNombre\tDireccion\n");
for (i=0;i<num;i++)
{
 
printf ("%ld\t\t",(p+i)->ncuenta);
printf ("%d\t",(p+i)->nip);
printf ("%ld\t",(p+i)->saldo);
printf ("%s\t",(p+i)->nombre);
printf ("%s\t",(p+i)->direccion);
printf ("\n");
fread(clientes,sizeof(clientes),1,parchivo);
}
fclose (parchivo);
}
break;
}
 
}
/*Termina switch principal*/
 
 
 
 
}
/*termina else*/
 
printf("Desea hacer otra transaccion?\n1)SI\n2)No\n");
scanf("%d",&op);
system("clear");
if (cantidad>0)
cantidad=cantidad+(cantidad*.02);
else
cantidad=cantidad-(cantidad*.04);
}while(op==1);
 
return 0;
}
 
 
int cambiar(int i,int A)
{
A=i;
return (A);
}
 
void leeropcion(int *opc)
{
scanf ("%d",opc);
return;
}
 
void menu()
{
printf("\n");
printf("░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░\n");
printf("░ ░\n");
printf("░ ░\n");
printf("░ 1).- RETIRO DE EFECTIVO 2).- CONSULTAR SALDO ░\n");
printf("░ 3).- TRASPASOS 4).- TIEMPO AIRE ░\n");
printf("░ 5).- CAMBIAR DE CUENTA 6).- SALIR ░\n");
printf("░ ░\n");
printf("░ ░\n");
printf("░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░\n");
printf("\n");
return;
}
 
void resta(struct clientes *c,int pos,int entero)
{
(c+pos)->saldo=(c+pos)->saldo-entero;
}
 
void escribir(struct clientes *c,int pos)
{
printf ("Nombre del usuario: %s\n",(c+pos)->nombre);
printf ("Numero de cuenta: %ld\n",(c+pos)->ncuenta);
printf("Su saldo es $%ld\n",(c+pos)->saldo);
}
 
void suma(struct clientes *c,int pos,int entero)
{
(c+pos)->saldo=(c+pos)->saldo+entero;
}
