// Archivos.cpp : Defines the entry point for the console application.
//

// archivo binario
#include "stdafx.h"
#include <iostream>
#include <stdio.h>
#include <conio.h>
#include<stdlib.h>
using namespace std;

struct regAgenda{
	char nombre[30];
	int edad;
	char email[80];
	char estado;
};

void crearArchivo(char nomArch[15])
{
	FILE *ptr;
	ptr= fopen(nomArch, "wb");//crea si no existe, si existe el contenido se pierde
	fclose(ptr);
}

void solicitarDatos(regAgenda *reg) //define un puntero a la variable reg
{
	cout<<endl<< "Introducir Nombre:";
	do{
		gets(reg->nombre);// reg.nombre --- reg->nombre 
	}while(strlen(reg->nombre) == 0);
	cout<< "Edad:";
	cin>> reg->edad;
	cout<<"Email:";	
	do{
		gets(reg->email);
	}while(strlen(reg->email) == 0);
	reg->estado='N';
}

void mostrarRegistro(regAgenda reg, int nroReg)
{
	cout<<endl<< nroReg<<".-"<< reg.nombre<< "         "<<reg.edad<< "    "<< reg.email;
}

void adicionarRegistro(char nomArch[15])
{
	FILE *ptr;
	regAgenda reg;
	ptr= fopen(nomArch, "ab");//abre el archivo y coloca el puntero al final del archivo 
	solicitarDatos(&reg);
	fwrite(&reg, sizeof(struct regAgenda),1,ptr);//escribe un registro en el archivo
	fclose(ptr);// cierra el archivo
}

void listarArchivo(char nomArch[15])
{
	FILE *ptr;
	regAgenda reg;
	int cont=0;
	ptr= fopen(nomArch,"rb");//abre el archivo para leer y el ptr queda en el 1er registro
	if(ptr == NULL)
	{
		cout<< "EL archivo no existe...";
	}
	else
	{
		cout<<endl<<"   ** LISTADO DE AMIGOS **";
		cout<<endl<<" Nombre      Edad      Email";
		cout<<endl<<"----------------------------";
		fread(&reg, sizeof(struct regAgenda),1,ptr);
		while(!feof(ptr))
		{
			if(reg.estado=='N')
			{
				mostrarRegistro(reg,cont+1);
			}
			fread(&reg, sizeof(struct regAgenda),1,ptr);//lee un registro del archivo
			cont++;
		}
		fclose(ptr);
	}
}

void buscarRegistro(char nomArch[15], int nroReg)
{
	FILE *ptr;
	regAgenda reg;
	ptr= fopen(nomArch,"rb");
	if(ptr== NULL)
	{
		cout<< "El archivo no existe...";
	}
	else
	{
		fseek(ptr, (nroReg-1)*sizeof(reg),SEEK_SET);//posiciona el ptr en un reg especifico
		fread(&reg, sizeof(struct regAgenda),1,ptr);
		if(feof(ptr))
			cout<<endl<< "Rrgistro no existe";
		else
			if(reg.estado=='N')
				mostrarRegistro(reg,nroReg);
			else
				cout<<endl<< "Registro eliminado...";
				fclose(ptr);
	}

}

void modificarRegistro(char nomArch[15], int nroReg)
{
	FILE *ptr;
	regAgenda reg;
	ptr= fopen(nomArch, "r+b");
	if(ptr== NULL)
	{
	cout<< "El archivo no existe...";
	}
else
	{
	fseek(ptr, (nroReg-1)*sizeof(reg),SEEK_SET);
	fread(&reg, sizeof(struct regAgenda),1,ptr);
		if(feof(ptr))
		{
			cout<<endl<< "Rrgistro no existe";
		}
		else
		{
		if(reg.estado=='N')
		{	mostrarRegistro(reg,nroReg);
			solicitarDatos(&reg);
			fseek(ptr, (nroReg-1)*sizeof(reg),SEEK_SET);
			fwrite(&reg, sizeof(struct regAgenda),1,ptr);
		}
		else
		{
			cout<<endl<< "Registro eliminado...";
			
		}
		fclose(ptr);
		}
	}
}

void eliminarRegistro(char nomArch[15], int nroReg)
{
	FILE *ptr;
	regAgenda reg;
	ptr= fopen(nomArch, "r+b");
	if(ptr== NULL)
	{
	cout<< "El archivo no existe...";
	}
else
	{
	fseek(ptr, (nroReg-1)*sizeof(reg),SEEK_SET);
	fread(&reg, sizeof(struct regAgenda),1,ptr);
		if(feof(ptr))
		{
			cout<<endl<< "Rrgistro no existe";
		}
		else
		{
		if(reg.estado=='N')
		{	mostrarRegistro(reg,nroReg);
			reg.estado= 'S';
			fseek(ptr, (nroReg-1)*sizeof(reg),SEEK_SET);
			fwrite(&reg, sizeof(struct regAgenda),1,ptr);
			cout<<endl<< "Registro eliminado exitosamente";
		}
		else
		{
			cout<<endl<< "Registro ya eliminado...";
			
		}
		fclose(ptr);
		}
	}
}

int main()
{int opcion;
	do{
		cout<<"\n****************MENU****************\n";
		cout<<"1.- Adicionar registro\n";
		cout<<"2.- Listar registro\n";
		cout<<"3.- Buscar registro\n";
		cout<<"4.- Modificar registro\n";
		cout<<"5.- Eliminar registros\n";
		cout<<"0.- Salir\n";
		cout<<"Elegir opcion:";
		cin>>opcion;
		switch(opcion){
			case 1:
				//crearArchivo("agenda.dat");
				adicionarRegistro("agenda.dat");
				getch();
				break;
			case 2:
				listarArchivo("agenda.dat");
				getch();
				break;
			case 3:
				int nro3;
				cout<<"Ingresar nro de registro:";
				cin>>nro3;
				buscarRegistro("agenda.dat",nro3);
				getch();
				break;
			case 4:
				int nro4;
				cout<<"Ingresar nro de registro:";
				cin>>nro4;
				modificarRegistro("agenda.dat",nro4);
				getch();
				break;
			case 5:
				int nro5;
				cout<<"Ingresar nro de registro:";
				cin>>nro5;
				eliminarRegistro("agenda.dat", nro5);
				getch();
				break;
			case 0:
				break;
			default:
				cout<<"Opcion invalida";
				getch();
				break;
		}
		system("cls");
	}while(opcion!=0);
	getch();
	return 0;

}
