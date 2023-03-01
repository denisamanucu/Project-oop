#include <iostream>
#include <fstream>
#include <string>
#include <conio.h>
#include <vector>
#include <map>
#include <set>
#include <list>
using namespace std;
#pragma warning(disable:4996)

//Domeniul: Activitatea unui targ

//Interfata
class IFile
{
public:
	virtual void writeToFile(fstream& file) = 0;
	virtual void readFromFile(fstream& file) = 0;
};

//Prima clasa
class Agentie : public IFile
{
private:
	char* denumireAgentie;
	char* tipAgentie;
	float pretAgentie;
	int durataContract;
	static int nrAgentie;
public:
	Agentie() {}
	Agentie(const char* denumireAgentie, const char* tipAgentie)
	{
		if (denumireAgentie != NULL)
		{
			this->denumireAgentie = new char[strlen(denumireAgentie) + 1];
			strcpy(this->denumireAgentie, denumireAgentie);
		}
		else
			this->denumireAgentie = NULL;

		if (tipAgentie != NULL)
		{
			this->tipAgentie = new char[strlen(tipAgentie) + 1];
			strcpy(this->tipAgentie, tipAgentie);
		}
		else
			this->tipAgentie = NULL;

		this->pretAgentie = 0;
		this->durataContract = 0;
	}
	Agentie(const char* denumireAgentie, const char* tipAgentie, float pretChirie, int durataContract)
	{
		if (denumireAgentie != NULL)
		{
			this->denumireAgentie = new char[strlen(denumireAgentie) + 1];
			strcpy(this->denumireAgentie, denumireAgentie);
		}
		else
			this->denumireAgentie = NULL;

		if (tipAgentie != NULL)
		{
			this->tipAgentie = new char[strlen(tipAgentie) + 1];
			strcpy(this->tipAgentie, tipAgentie);
		}
		else
			this->tipAgentie = NULL;

		this->pretAgentie = pretAgentie;

		if (durataContract > 0)
			this->durataContract = durataContract;
		else
			this->durataContract = 0;

		nrAgentie++;

	}
	Agentie(const Agentie& s)
	{
		if (s.denumireAgentie != NULL)
		{
			this->denumireAgentie = new char[strlen(s.denumireAgentie) + 1];
			strcpy(this->denumireAgentie, s.denumireAgentie);
		}
		else
			this->denumireAgentie = NULL;

		if (s.tipAgentie != NULL)
		{
			this->tipAgentie = new char[strlen(s.tipAgentie) + 1];
			strcpy(this->tipAgentie, s.tipAgentie);
		}
		else
			this->tipAgentie = NULL;

		if (s.pretAgentie > 0)
			this->pretAgentie = s.pretAgentie;
		else
			this->pretAgentie = 0;

		if (s.durataContract > 0)
			this->durataContract = s.durataContract;
		else
			this->durataContract = 0;
		nrAgentie++;
	}
	~Agentie()
	{
		delete[] this->denumireAgentie;
		delete[] this->tipAgentie;
		nrAgentie--;
	}
	Agentie& operator=(const Agentie& s)
	{
		delete[]this->denumireAgentie;
		if (s.denumireAgentie != NULL)
		{
			this->denumireAgentie = new char[strlen(s.denumireAgentie) + 1];
			strcpy(this->denumireAgentie, s.denumireAgentie);
		}
		else
			this->denumireAgentie = NULL;

		delete[]this->tipAgentie;
		if (s.tipAgentie != NULL)
		{
			this->tipAgentie = new char[strlen(s.tipAgentie) + 1];
			strcpy(this->tipAgentie, s.tipAgentie);
		}
		else
			this->tipAgentie = NULL;

		if (s.pretAgentie > 0)
			this->pretAgentie = s.pretAgentie;
		else
			this->pretAgentie = 0;

		if (s.durataContract > 0)
			this->durataContract = s.durataContract;
		else
			this->durataContract = 0;

		nrAgentie++;
		return *this;
	}

	char* getdenumireAgentie()
	{
		return this->denumireAgentie;
	}

	char* gettipAgentie()
	{
		return this->tipAgentie;
	}
	float getpretAgentie()
	{
		return this->pretAgentie;
	}
	int getdurataContract()
	{
		return this->durataContract;
	}

	void setdenumireAgentie(const char* agentie)
	{
		if (strlen(agentie) > 0)
		{
			if (this->denumireAgentie == NULL)
				this->denumireAgentie = _strdup(agentie);
			else
			{
				delete[]this->denumireAgentie;
				this->denumireAgentie = _strdup(agentie);
			}
		}
		else
			cout << "Denumire invalida";
	}
	void settipAgentie(const char* tip)
	{
		if (strlen(tip) > 0)
		{
			if (this->tipAgentie == NULL)
				this->tipAgentie = _strdup(tip);
			else
			{
				delete[]this->tipAgentie;
				this->tipAgentie = _strdup(tip);
			}
		}
		else
			cout << "Tip invalid";
	}
	void setpretAgentie(float p)
	{
		if (p != 0)
			pretAgentie = p;
		else
			cout << "Pret invalid!" << endl;
	}
	void setdurataContract(int d)
	{
		if (d != 0)
			durataContract = d;
		else
			cout << "Durata contract invalida!" << endl;
	}

	//Metoda pentru a vedea daca pretul agentiei este mai mare decat 100
	bool consultarepretAgentie()
	{
		if (pretAgentie > 100)
			return true;
		else
			return false;
	}

	//Operatorul index [];
	char operator[](int index) {
		if (this->tipAgentie != NULL)
			return this->tipAgentie[index];
		else
			cout << "Indexul introdus e gresit";
	}
	//Operatorul *
	Agentie operator *(float curslei)
	{
		this->pretAgentie = this->pretAgentie * curslei;
		return *this;
	}

	//Operatorul ++ Forma de preincrementare
	Agentie operator++(int)
	{
		this->pretAgentie++;
		return *this;
	}
	//Operatorul ++ Forma de postincrementare
	Agentie operator++()
	{
		Agentie st = *this;
		this->pretAgentie++;
		return st;
	}
	//Operator cast
	operator int()
	{
		return this->durataContract;
	}

	//Operator !
	bool operator!()
	{
		if (this->durataContract != 0)
			return true;
		else
			return false;
	}
	//Operator <
	bool operator<(Agentie& s)
	{
		if (this->pretAgentie < s.pretAgentie)
			return true;
		else
			return false;
	}
	//Operatorul ==
	bool operator==(const Agentie& s)
	{
		if (this->pretAgentie == s.pretAgentie)
			return true;
		else
			return false;
	}

	void writeToFile(fstream& file)
	{
		//char*
		int lg = strlen(this->denumireAgentie) + 1;
		file.write((char*)&lg, sizeof(int));
		file.write(this->denumireAgentie, lg);
		//char*
		int lg2 = strlen(this->tipAgentie) + 1;
		file.write((char*)&lg2, sizeof(int));
		file.write(this->tipAgentie, lg2);
		//float pretChirie
		file.write((char*)&this->pretAgentie, sizeof(float));
		//int durataContract
		file.write((char*)&this->durataContract, sizeof(int));
	}

	void readFromFile(fstream& file)
	{
		//citire nume(char*);
		delete[] this->denumireAgentie;
		int lg = 0;
		file.read((char*)&lg, sizeof(int));
		this->denumireAgentie = new char[lg];
		file.read(this->denumireAgentie, lg);

		delete[] this->tipAgentie;
		int lg2 = 0;
		file.read((char*)&lg2, sizeof(int));
		this->tipAgentie = new char[lg2];
		file.read(this->tipAgentie, lg2);
		//citire float pretAgentie
		file.read((char*)&this->pretAgentie, sizeof(float));
		//citire int durataContract
		file.read((char*)&this->durataContract, sizeof(int));
	}

	friend ostream& operator<<(ostream& out, const Agentie& s);
	friend istream& operator>>(istream& in, Agentie& s);
	friend ofstream& operator<<(ofstream& out, const Agentie& s);
	friend ifstream& operator>>(ifstream& in, Agentie& s);

};
ostream& operator<<(ostream& out, const Agentie& s)
{
	out << "Denumirea agentiei: " << s.denumireAgentie << endl;
	out << "Tipul de agentie: " << s.tipAgentie << endl;
	out << "Pret agentie: " << s.pretAgentie << endl;
	out << "Durata contractului:  " << s.durataContract << endl;
	return out;
}
istream& operator>>(istream& in, Agentie& s)
{
	char denumireSt[10];
	if (s.denumireAgentie != NULL)
		delete[]s.denumireAgentie;
	cout << "Denumirea agentiei: ";
	in >> denumireSt;
	s.denumireAgentie = new char[strlen(denumireSt) + 1];
	strcpy(s.denumireAgentie, denumireSt);
	char tip[10];
	if (s.tipAgentie != NULL)
		delete[]s.tipAgentie;
	cout << "Tipul agentiei: ";
	in >> tip;
	s.tipAgentie = new char[strlen(tip) + 1];
	strcpy(s.tipAgentie, tip);
	cout << "Pretul agentiei: ";
	in >> s.pretAgentie;
	cout << "Durata contractului: ";
	in >> s.durataContract;
	return in;
}
ofstream& operator<<(ofstream& g, const Agentie& s)
{
	g << s.denumireAgentie << ",";
	g << s.tipAgentie << ",";
	g << s.pretAgentie << ",";
	g << s.durataContract << ",";
	return g;
}
ifstream& operator>>(ifstream& f, Agentie& s)
{
	delete[]s.denumireAgentie;
	delete[]s.tipAgentie;
	char denumireSt[10];
	f >> denumireSt;
	s.denumireAgentie = new char[strlen(denumireSt) + 1];
	strcpy(s.denumireAgentie, denumireSt);
	char tip[10];
	f >> tip;
	s.tipAgentie = new char[strlen(tip) + 1];
	strcpy(s.tipAgentie, tip);
	f >> s.pretAgentie;
	f >> s.durataContract;
	return f;

}

int Agentie::nrAgentie = 0;

//A doua clasa
class Designer : public IFile
{
private:
	char* numeDesigner;
	int varsta;
	int experienta;
	char* orasulProvenienta;

public:
	Designer() {};
	Designer(const char* numeDesigner, const char* orasulProvenienta)
	{
		if (numeDesigner != NULL)
		{
			this->numeDesigner = new char[strlen(numeDesigner) + 1];
			strcpy(this->numeDesigner, numeDesigner);
		}
		else
			this->numeDesigner = NULL;

		if (orasulProvenienta != NULL)
		{
			this->orasulProvenienta = new char[strlen(orasulProvenienta) + 1];
			strcpy(this->orasulProvenienta, orasulProvenienta);
		}
		else
			this->orasulProvenienta = NULL;

		this->varsta = 0;
		this->experienta = 0;


	}
	Designer(const char* numeDesigner, int varsta, int experienta, const char* orasulProvenienta)
	{
		if (numeDesigner != NULL)
		{
			this->numeDesigner = new char[strlen(numeDesigner) + 1];
			strcpy(this->numeDesigner, numeDesigner);
		}
		else
			this->numeDesigner = NULL;

		if (varsta > 0)
			this->varsta = varsta;
		else
			this->varsta = 0;

		if (experienta > 0)
			this->experienta = experienta;
		else
			this->experienta = 0;

		if (orasulProvenienta != NULL)
		{
			this->orasulProvenienta = new char[strlen(orasulProvenienta) + 1];
			strcpy(this->orasulProvenienta, orasulProvenienta);
		}
		else
			this->orasulProvenienta = NULL;


	}
	Designer(const Designer& c)
	{
		if (c.numeDesigner != NULL)
		{
			this->numeDesigner = new char[strlen(c.numeDesigner) + 1];
			strcpy(this->numeDesigner, c.numeDesigner);
		}
		else
			this->numeDesigner = NULL;

		if (c.varsta > 0)
			this->varsta = c.varsta;
		else
			this->varsta = 0;

		if (c.experienta > 0)
			this->experienta = c.experienta;
		else
			this->experienta = 0;

		if (c.orasulProvenienta != NULL)
		{
			this->orasulProvenienta = new char[strlen(c.orasulProvenienta) + 1];
			strcpy(this->orasulProvenienta, c.orasulProvenienta);
		}
		else
			this->orasulProvenienta = NULL;

	}
	~Designer()
	{
		delete[] this->numeDesigner;
		delete[]this->orasulProvenienta;
	}
	Designer& operator=(const Designer& c)
	{
		delete[]this->numeDesigner;
		if (c.numeDesigner != NULL)
		{
			this->numeDesigner = new char[strlen(c.numeDesigner) + 1];
			strcpy(this->numeDesigner, c.numeDesigner);
		}
		else
			this->numeDesigner = NULL;

		if (c.varsta > 0)
			this->varsta = c.varsta;
		else
			this->varsta = 0;

		if (c.experienta > 0)
			this->experienta = c.experienta;
		else
			this->experienta = 0;

		if (c.orasulProvenienta != NULL)
		{
			this->orasulProvenienta = new char[strlen(c.orasulProvenienta) + 1];
			strcpy(this->orasulProvenienta, c.orasulProvenienta);
		}
		else
			this->orasulProvenienta = NULL;


		return *this;
	}

	char* getnumeDesigner()
	{
		return this->numeDesigner;
	}
	int getvarsta()
	{
		return this->varsta;
	}
	int getexperienta()
	{
		return this->experienta;
	}
	char* getorasulProvenienta()
	{
		return this->orasulProvenienta;
	}

	void setnumeDesigner(const char* designer)
	{
		if (strlen(designer) > 0)
		{
			if (this->numeDesigner == NULL)
				this->numeDesigner = _strdup(designer);
			else
			{
				delete[]this->numeDesigner;
				this->numeDesigner = _strdup(designer);
			}
		}
		else
			cout << "Nume invalid";
	}
	void setvarsta(int v)
	{
		if (v > 18)
			varsta = v;
		else
			cout << "Minor!";
	}
	void setexperienta(int e)
	{
		if (e > 10)
			experienta = e;
		else
			cout << "Fara experienta";
	}
	void setorasulProvenienta(const char* provenire)
	{
		if (strlen(provenire) > 0)
		{
			if (this->orasulProvenienta == NULL)
				this->orasulProvenienta = _strdup(provenire);
			else
			{
				delete[]this->orasulProvenienta;
				this->orasulProvenienta = _strdup(provenire);
			}
		}
		else
			cout << "Provenienta invalida";

	}
	//Operatorul index [];
	char operator[](int index) {
		if (this->numeDesigner != NULL)
			return this->numeDesigner[index];
		else
			cout << "Indexul introdus e gresit";
	}

	// Operatorul /
	Designer operator /(int x)
	{
		this->experienta = this->experienta / x;
		return *this;
	}

	//Operatorul ++ Forma de preincrementare
	Designer operator--(int)
	{
		this->experienta--;
		return *this;
	}

	//Operatorul ++ Forma de postincrementare
	Designer operator--()
	{
		Designer c = *this;
		this->experienta--;
		return c;
	}

	//Operator cast
	operator int()
	{
		return this->experienta;
	}

	//Operator !
	bool operator!()
	{
		if (this->varsta != 0)
			return true;
		else
			return false;
	}

	//Operator >
	bool operator>(Designer& c)
	{
		if (this->varsta > c.varsta)
			return true;
		else
			return false;
	}
	//Operator ==
	bool operator==(const Designer& c)
	{
		if (this->varsta == c.varsta)
			return true;
		else
			return false;
	}
	void writeToFile(fstream& file)
	{
		//char*
		int lg = strlen(this->numeDesigner) + 1;
		file.write((char*)&lg, sizeof(int));
		file.write(this->numeDesigner, lg);
		//int varsta
		file.write((char*)&this->varsta, sizeof(int));
		//int experienta
		file.write((char*)&this->experienta, sizeof(int));
		//char* provenienta
		int lg2 = strlen(this->orasulProvenienta) + 1;
		file.write((char*)&lg2, sizeof(int));
		file.write(this->orasulProvenienta, lg2);
	}

	void readFromFile(fstream& file)
	{
		//citire char* numeComerciant
		delete[] this->numeDesigner;
		int size = 0;
		file.read((char*)&size, sizeof(int));
		this->numeDesigner = new char[size];
		file.read(this->numeDesigner, size);
		//citire int varsta
		file.read((char*)&this->varsta, sizeof(int));
		//citire int experienta
		file.read((char*)&this->experienta, sizeof(int));

		delete[] this->orasulProvenienta;
		int size2 = 0;
		file.read((char*)&size2, sizeof(int));
		this->orasulProvenienta = new char[size2];
		file.read(this->orasulProvenienta, size2);

	}
	friend ostream& operator<<(ostream& out, const Designer& c);
	friend istream& operator>>(istream& in, Designer& c);
	friend ofstream& operator<<(ofstream& out, const Designer& c);
	friend ifstream& operator>>(ifstream& in, Designer& c);
};
ostream& operator<<(ostream& out, const Designer& c)
{
	out << "Nume designer: " << c.numeDesigner << endl;
	out << "Varsta: " << c.varsta << endl;
	out << "Experienta: " << c.experienta << endl;
	out << " Oras de provenienta: " << c.orasulProvenienta << endl;
	return out;
}
istream& operator>>(istream& in, Designer& c)
{
	char nume[10];
	if (c.numeDesigner != NULL)
		delete[]c.numeDesigner;
	cout << "Nume designer: ";
	in >> nume;
	c.numeDesigner = new char[strlen(nume) + 1];
	strcpy(c.numeDesigner, nume);
	cout << "Varsta : ";
	in >> c.varsta;
	cout << "Experienta: ";
	in >> c.experienta;
	char provenientaC[10];
	if (c.orasulProvenienta != NULL)
		delete[]c.orasulProvenienta;
	cout << "Orasul de provenienta: ";
	in >> provenientaC;
	c.orasulProvenienta = new char[strlen(provenientaC) + 1];
	strcpy(c.orasulProvenienta, provenientaC);
	return in;
}
ofstream& operator<<(ofstream& g2, const Designer& c)
{
	g2 << c.numeDesigner << ",";
	g2 << c.varsta << ",";
	g2 << c.experienta << ",";
	g2 << c.orasulProvenienta << ",";
	return g2;
}
ifstream& operator>>(ifstream& f2, Designer& c)
{
	delete[]c.numeDesigner;
	delete[]c.orasulProvenienta;
	char nume[10];
	f2 >> nume;
	c.numeDesigner = new char[strlen(nume) + 1];
	strcpy(c.numeDesigner, nume);
	f2 >> c.varsta;
	f2 >> c.experienta;
	char provenientaC[10];
	f2 >> provenientaC;
	c.orasulProvenienta = new char[strlen(provenientaC) + 1];
	strcpy(c.orasulProvenienta, provenientaC);
	return f2;

}
//invitati
//A treia clasa
class Invitat
{
protected:
	char* numeInvitat;
	int varstaInvitat;
	int marime;
	float soldBugetAlocat;
public:
	Invitat() {}
	Invitat(const char* numeInvitat, int varstaInvitat)
	{
		if (numeInvitat != NULL)
		{
			this->numeInvitat = new char[strlen(numeInvitat) + 1];
			strcpy(this->numeInvitat, numeInvitat);
		}
		else
			this->numeInvitat = NULL;

		if (varstaInvitat > 0)
			this->varstaInvitat = varstaInvitat;
		else
			this->varstaInvitat = 0;

		this->marime = 0;
		this->soldBugetAlocat = 0;

	}
	Invitat(const char* numeInvitat, int varstaInvitat, int marime, float soldBugetAlocat)
	{
		if (numeInvitat != NULL)
		{
			this->numeInvitat = new char[strlen(numeInvitat) + 1];
			strcpy(this->numeInvitat, numeInvitat);
		}
		else
			this->numeInvitat = NULL;

		if (varstaInvitat > 0)
			this->varstaInvitat = varstaInvitat;
		else
			this->varstaInvitat = 0;

		if (marime > 0)
			this->marime = marime;
		else
			this->marime = 0;

		if (soldBugetAlocat > 0)
			this->soldBugetAlocat = soldBugetAlocat;
		else
			this->soldBugetAlocat = 0;

	}
	Invitat(const Invitat& i)
	{
		if (i.numeInvitat != NULL)
		{
			this->numeInvitat = new char[strlen(i.numeInvitat) + 1];
			strcpy(this->numeInvitat, i.numeInvitat);
		}
		else
			this->numeInvitat = NULL;

		if (i.varstaInvitat > 0)
			this->varstaInvitat = i.varstaInvitat;
		else
			this->varstaInvitat = 0;

		if (i.marime > 0)
			this->marime = i.marime;
		else
			this->marime = 0;

		if (i.soldBugetAlocat > 0)
			this->soldBugetAlocat = i.soldBugetAlocat;
		else
			this->soldBugetAlocat = 0;

	}
	~Invitat()
	{
		delete[] this->numeInvitat;
	}
	Invitat& operator=(const Invitat& i)
	{
		delete[]this->numeInvitat;
		if (i.numeInvitat != NULL)
		{
			this->numeInvitat = new char[strlen(i.numeInvitat) + 1];
			strcpy(this->numeInvitat, i.numeInvitat);
		}
		else
			this->numeInvitat = NULL;

		if (i.varstaInvitat > 0)
			this->varstaInvitat = i.varstaInvitat;
		else
			this->varstaInvitat = 0;

		if (i.marime > 0)
			this->marime = i.marime;
		else
			this->marime = 0;

		if (i.soldBugetAlocat > 0)
			this->soldBugetAlocat = i.soldBugetAlocat;
		else
			this->soldBugetAlocat = 0;

		return *this;
	}

	char* getnumeInvitat()
	{
		return this->numeInvitat;
	}
	int getvarstaInvitat()
	{
		return this->varstaInvitat;
	}
	int getmarime()
	{
		return this->marime;
	}
	float getsoldBuget()
	{
		return this->soldBugetAlocat;
	}

	void setnumeInvitat(const char* invitat)
	{
		if (strlen(invitat) > 0)
		{
			if (this->numeInvitat == NULL)
				this->numeInvitat = _strdup(invitat);
			else
			{
				delete[]this->numeInvitat;
				this->numeInvitat = _strdup(invitat);
			}
		}
		else
			cout << "Nume invalid";
	}
	void setvarstainvitat(int v)
	{
		if (v > 18)
			varstaInvitat = v;
		else
			cout << "Persoana nu este majora!";
	}
	void setmarime(int m)
	{
		if (m > 0)
			marime = m;
		else
			cout << "Marime gresita!" << endl;
	}
	void setsoldBuget(float s)
	{
		if (s > 0)
			soldBugetAlocat = s;
		else
			cout << "Sold buget gresit!" << endl;
	}
	//Metoda pentru a vedea daca soldul bugetului este mai mic decat 50
	bool consultareSold()
	{
		if (soldBugetAlocat < 50)
			return true;
		else
			return false;
	}

	//Operatorul index [];
	char operator[](int index) {
		if (this->numeInvitat != NULL)
			return this->numeInvitat[index];
		else
			cout << "Indexul introdus e gresit";
	}
	//Operatorul +
	Invitat operator+(int m)
	{
		this->marime = this->marime + m;
		return *this;
	}
	//Operatorul ++ Forma de preincrementare
	Invitat operator++(int)
	{
		this->marime++;
		return *this;
	}
	//Operatorul ++ Forma de postincrementare
	Invitat operator++()
	{
		Invitat i = *this;
		this->marime++;
		return i;
	}
	//Operator cast
	operator int()
	{
		return this->varstaInvitat;
	}

	//Operator !
	bool operator!()
	{
		if (this->marime != 0)
			return true;
		else
			return false;
	}
	//Operator <=
	bool operator<=(Invitat& i)
	{
		if (this->varstaInvitat <= i.varstaInvitat)
			return true;
		else
			return false;
	}
	//Operator ==
	bool operator==(const Invitat& i)
	{
		if (this->varstaInvitat == i.varstaInvitat)
			return true;
		else
			return false;
	}
	void writeToFile(fstream& file)
	{
		//char*
		int lg = strlen(this->numeInvitat) + 1;
		file.write((char*)&lg, sizeof(int));
		file.write(this->numeInvitat, lg);
		//int varstaClient
		file.write((char*)&this->varstaInvitat, sizeof(int));
		//int marime
		file.write((char*)&this->marime, sizeof(int));
		//float soldBuget
		file.write((char*)&this->soldBugetAlocat, sizeof(float));
	}

	void readFromFile(fstream& file)
	{
		//citire char* numeClient
		delete[] this->numeInvitat;
		int lg = 0;
		file.read((char*)&lg, sizeof(int));
		this->numeInvitat = new char[lg];
		file.read(this->numeInvitat, lg);
		//citire int varstaClient
		file.read((char*)&this->varstaInvitat, sizeof(int));
		//citire int marime
		file.read((char*)&this->marime, sizeof(int));
		//citire float soldBuget
		file.read((char*)&this->soldBugetAlocat, sizeof(float));

	}

	friend ostream& operator<<(ostream& out, const Invitat& cl);
	friend istream& operator>>(istream& in, Invitat& cl);
	friend ofstream& operator<<(ofstream& out, const Invitat& cl);
	friend ifstream& operator>>(ifstream& in, Invitat& cl);


};
ostream& operator<<(ostream& out, const Invitat& cl)
{
	out << "Numele invitatului: " << cl.numeInvitat << endl;
	out << "Varsta invitatului: " << cl.varstaInvitat << endl;
	out << "Marimea invitatului: " << cl.marime << endl;
	out << "Soldul bugetului alocat pentru invitat: " << cl.soldBugetAlocat << endl;
	return out;
}
istream& operator>>(istream& in, Invitat& cl)
{
	char numecl[10];
	if (cl.numeInvitat != NULL)
		delete[]cl.numeInvitat;
	cout << "Numele invitatului: ";
	in >> numecl;
	cl.numeInvitat = new char[strlen(numecl) + 1];
	strcpy(cl.numeInvitat, numecl);
	cout << "Varsta invitatului: ";
	in >> cl.varstaInvitat;
	cout << "Marimea invitatului: ";
	in >> cl.marime;
	cout << "Soldul bugetului alocat pentru invitat: ";
	in >> cl.soldBugetAlocat;
	return in;
}
ofstream& operator<<(ofstream& g3, const Invitat& cl)
{
	g3 << cl.numeInvitat << ",";
	g3 << cl.varstaInvitat << ",";
	g3 << cl.marime << ",";
	g3 << cl.soldBugetAlocat << ",";
	return g3;
}
ifstream& operator>>(ifstream& f3, Invitat& cl)
{
	delete[]cl.numeInvitat;
	char numecl[10];
	f3 >> numecl;
	cl.numeInvitat = new char[strlen(numecl) + 1];
	strcpy(cl.numeInvitat, numecl);
	f3 >> cl.varstaInvitat;
	f3 >> cl.marime;
	f3 >> cl.soldBugetAlocat;
	return f3;

}

//Has a
class locMasa
{
	int nr_loc;
	vector<	Invitat*> invitati;
public:
	locMasa()
	{
		this->nr_loc = 0;
	}

	locMasa(int nr_loc)
	{
		this->nr_loc = nr_loc;
	}

	locMasa(const locMasa& p)
	{
		this->nr_loc = p.nr_loc;
		this->invitati = p.invitati;
	}

	~locMasa()
	{
		nr_loc = 0;

		for (int i = 0; i < invitati.size(); i++)
			invitati.pop_back();
	}

	void add_invitat(Invitat* c)
	{
		this->invitati.push_back(c);
	}

	friend ostream& operator<<(ostream& out, const locMasa& p)
	{
		out << "\nNumarul locului: " << p.nr_loc << endl;

		out << "Lista invitatilor:" << endl;
		for (int i = 0; i < p.invitati.size(); i++)
			out << p.invitati[i]->getnumeInvitat() << " cu varsta " << p.invitati[i]->getvarstaInvitat() << ", marimea " << p.invitati[i]->getmarime() << " si soldul " << p.invitati[i]->getsoldBuget() << endl;
		return out;
	}

};

//A patra clasa
class Articol
{
protected:
	char* denumirearticol;
	const int codarticol;
	float pretarticol;
	int cantitate;
	char* datafabricatie;
public:
	Articol() :codarticol(codarticol) {}
	Articol(const char* denumirearticol, const char* datafabricatie) :codarticol(codarticol)
	{
		if (denumirearticol != NULL)
		{
			this->denumirearticol = new char[strlen(denumirearticol) + 1];
			strcpy(this->denumirearticol, denumirearticol);
		}
		else
			this->denumirearticol = NULL;

		if (datafabricatie != NULL)
		{
			this->datafabricatie = new char[strlen(datafabricatie) + 1];
			strcpy(this->datafabricatie, datafabricatie);
		}
		else
			this->datafabricatie = NULL;

		this->pretarticol = 0;
		this->cantitate = 0;
	}
	Articol(const char* denumirearticol, int codarticol, float pretarticol, int cantitate, const char* datafabricatie) :codarticol(codarticol)
	{
		if (denumirearticol != NULL)
		{
			this->denumirearticol = new char[strlen(denumirearticol) + 1];
			strcpy(this->denumirearticol, denumirearticol);
		}
		else
			this->denumirearticol = NULL;

		if (pretarticol > 0)
			this->pretarticol = pretarticol;
		else
			this->pretarticol = 0;

		if (cantitate > 0)
			this->cantitate = cantitate;
		else
			this->cantitate = 0;

		if (datafabricatie != NULL)
		{
			this->datafabricatie = new char[strlen(datafabricatie) + 1];
			strcpy(this->datafabricatie, datafabricatie);
		}
		else
			this->datafabricatie = NULL;

	}
	Articol(const Articol& p) :codarticol(p.codarticol)
	{
		if (p.denumirearticol != NULL)
		{
			this->denumirearticol = new char[strlen(p.denumirearticol) + 1];
			strcpy(this->denumirearticol, p.denumirearticol);
		}
		else
			this->denumirearticol = NULL;

		if (p.pretarticol > 0)
			this->pretarticol = p.pretarticol;
		else
			this->pretarticol = 0;

		if (p.cantitate > 0)
			this->cantitate = p.cantitate;
		else
			this->cantitate = 0;

		if (p.datafabricatie != NULL)
		{
			this->datafabricatie = new char[strlen(p.datafabricatie) + 1];
			strcpy(this->datafabricatie, p.datafabricatie);
		}
		else
			this->datafabricatie = NULL;
	}
	~Articol()
	{
		delete[] this->denumirearticol;
	}
	Articol& operator=(const Articol& p)
	{
		delete[]this->denumirearticol;
		if (p.denumirearticol != NULL)
		{
			this->denumirearticol = new char[strlen(p.denumirearticol) + 1];
			strcpy(this->denumirearticol, p.denumirearticol);
		}
		else
			this->denumirearticol = NULL;

		if (p.pretarticol > 0)
			this->pretarticol = p.pretarticol;
		else
			this->pretarticol = 0;

		if (p.cantitate > 0)
			this->cantitate = p.cantitate;
		else
			this->cantitate = 0;

		for (int i = 0; i < p.cantitate; i++)
			if (p.datafabricatie[i] > 0)
				this->datafabricatie[i] = p.datafabricatie[i];
			else
				this->datafabricatie[i] = 0;
		return *this;
	}

	char* getdenumireArticol()
	{
		return this->denumirearticol;
	}

	float getpretArticol()
	{
		return this->pretarticol;
	}
	int getcantitate()
	{
		return this->cantitate;
	}
	char* getdatafabricatie()
	{
		return this->datafabricatie;
	}

	void setdenumirearticol(const char* articol)
	{
		if (strlen(articol) > 0)
		{
			if (this->denumirearticol == NULL)
				this->denumirearticol = _strdup(articol);
			else
			{
				delete[]this->denumirearticol;
				this->denumirearticol = _strdup(articol);
			}
		}
		else
			cout << "Denumire invalida";
	}
	void setpretarticol(float c)
	{
		if (c > 0)
			pretarticol = c;
		else
			cout << "Pret gresit!" << endl;
	}
	void setcantitate(int cantitate1)
	{
		if (cantitate1 > 0)
			cantitate = cantitate1;
		else
			cout << "Cantitate gresita!" << endl;
	}

	void setdatafabricatie(const char* df)
	{
		if (strlen(df) > 0)
			strcpy(datafabricatie, df);
		else
			cout << "Data de fabricatie introdusa gresit!";
	}
	//Operatorul index [];
	char operator[](int index) {
		if (this->denumirearticol != NULL)
			return this->denumirearticol[index];
		else
			cout << "Indexul introdus e gresit";
	}
	//Operatorul /
	Articol operator+(int timp)
	{
		this->cantitate = this->cantitate / timp;
		return *this;
	}
	//Operatorul ++ Forma de preincrementare
	Articol operator++(int)
	{
		this->cantitate++;
		return *this;
	}
	//Operatorul ++ Forma de postincrementare
	Articol operator++()
	{
		Articol p = *this;
		this->cantitate++;
		return p;
	}
	//Operator cast
	operator int()
	{
		return this->pretarticol;
	}

	//Operator !
	bool operator!()
	{
		if (this->cantitate != 0)
			return true;
		else
			return false;
	}
	//Operator <=
	bool operator<=(Articol& p)
	{
		if (this->pretarticol <= p.pretarticol)
			return true;
		else
			return false;
	}
	//Operatorul ==
	bool operator==(const Articol& p)
	{
		if (this->pretarticol == p.pretarticol)
			return true;
		else
			return false;
	}


	void writeToFile(fstream& file)
	{
		//char*
		int lg = strlen(this->denumirearticol) + 1;
		file.write((char*)&lg, sizeof(int));
		file.write(this->denumirearticol, lg);

		file.write((char*)&this->pretarticol, sizeof(float));
		//int cantitate
		file.write((char*)&this->cantitate, sizeof(int));
		//char*
		int lg2 = strlen(this->datafabricatie) + 1;
		file.write((char*)&lg2, sizeof(int));
		file.write(this->datafabricatie, lg2);
	}

	void readFromFile(fstream& file)
	{

		delete[] this->denumirearticol;
		int lg = 0;
		file.read((char*)&lg, sizeof(int));
		this->denumirearticol = new char[lg];
		file.read(this->denumirearticol, lg);

		file.read((char*)&this->pretarticol, sizeof(float));
		//citire int cantitate
		file.read((char*)&this->cantitate, sizeof(int));

		delete[] this->datafabricatie;
		int lg2 = 0;
		file.read((char*)&lg2, sizeof(int));
		this->datafabricatie = new char[lg2];
		file.read(this->datafabricatie, lg2);
	}

	virtual float calculpretarticol()
	{
		return this->pretarticol;
	}

	friend ostream& operator<<(ostream& out, const Articol& p);
	friend istream& operator>>(istream& in, Articol& p);
	friend ofstream& operator<<(ofstream& g, const Articol& p);
	friend ifstream& operator>>(ifstream& f, Articol& p);

};
ostream& operator<<(ostream& out, const Articol& p)
{
	out << "Denumirea produsului: " << p.denumirearticol << endl;
	out << "Pretul este de: " << p.pretarticol << endl;
	out << "Cantitatea este de: " << p.cantitate << endl;
	out << "Termenul de valabilitate este: " << p.datafabricatie << endl;
	return out;
}
istream& operator>>(istream& in, Articol& p)
{
	char denumire[15];
	char datafabricatie[20];
	if (p.denumirearticol != NULL)
		delete[]p.denumirearticol;
	cout << "Denumirea articolului: ";
	in >> denumire;
	p.denumirearticol = new char[strlen(denumire) + 1];
	strcpy(p.denumirearticol, denumire);
	cout << "Pretul: ";
	in >> p.pretarticol;
	cout << "Cantitatea : ";
	in >> p.cantitate;
	if (p.datafabricatie != NULL)
		delete[] p.datafabricatie;
	cout << "Data fabricatiei:";
	in >> datafabricatie;
	p.datafabricatie = _strdup(datafabricatie);
	return in;
}
ofstream& operator<<(ofstream& g4, const Articol& p)
{
	g4 << p.denumirearticol << ",";
	g4 << p.pretarticol << ",";
	g4 << p.cantitate << ",";
	g4 << p.codarticol << ",";
	return g4;
}
ifstream& operator>>(ifstream& f4, Articol& p)
{
	delete[]p.denumirearticol;
	delete[] p.datafabricatie;
	char denumire[15];
	f4 >> denumire;
	p.denumirearticol = new char[strlen(denumire) + 1];
	strcpy(p.denumirearticol, denumire);
	f4 >> p.pretarticol;
	f4 >> p.cantitate;
	char datafabricatie[20];
	f4 >> datafabricatie;
	p.datafabricatie = new char[strlen(datafabricatie) + 1];
	strcpy(p.datafabricatie, datafabricatie);
	return f4;
}
//	Articol(const char* denumirearticol, int codarticol, float pretarticol, int cantitate, const char* datafabricatie) :codarticol(codarticol)
//Is a
class Rochie : public Articol
{
private:
	int nr_culori;
public:
	Rochie() :Articol()
	{
		this->nr_culori = 0;
	}
	Rochie(const char* da, int ca, float pa, int c, const char* dfa, int nc) :Articol(da, ca, pa, c, dfa)
	{
		this->nr_culori = nc;
	}
	Rochie(const Rochie& m) :Articol(m)
	{
		this->nr_culori = m.nr_culori;
	}
	Rochie& operator=(const Rochie& m)
	{
		this->nr_culori = m.nr_culori;
		return *this;
	}
	~Rochie()
	{
	}

	friend ostream& operator<<(ostream& out, const Rochie& m)
	{
		out << "\nNumarul culorilor: " << m.nr_culori;
		return out;
	}
	float calculpretarticol()
	{
		return this->pretarticol * this->nr_culori;
	}

};
class Pantaloni : public Articol
{
private:
	int nr_materiale;
public:
	Pantaloni() :Articol()
	{
		this->nr_materiale = 0;
	}
	Pantaloni(const char* d, int cP, float p, int c, const char* t, int s) :Articol(d, cP, p, c, t)
	{
		this->nr_materiale = s;
	}
	Pantaloni(const Pantaloni& o) :Articol(o)
	{
		this->nr_materiale = o.nr_materiale;
	}
	Pantaloni& operator=(const Pantaloni& f)
	{
		this->nr_materiale = f.nr_materiale;
		return *this;
	}
	friend ostream& operator<<(ostream& out, const Pantaloni& f)
	{
		out << "\nNumarul materialelor: " << f.nr_materiale;
		return out;
	}
	~Pantaloni()
	{
	}

	float calculpretarticol()
	{
		return this->pretarticol * this->nr_materiale;
	}

};
//sponsor

class Sponsor
{
private:
	char* numeSponsor;
	char domeniuFirma[20];
	float perioadaSponsorizare;
public:
	Sponsor() {}
	Sponsor(const char* numeSponsor, const char domeniuFirma[20])
	{
		if (numeSponsor != NULL)
		{
			this->numeSponsor = new char[strlen(numeSponsor) + 1];
			strcpy(this->numeSponsor, numeSponsor);
		}
		else
			this->numeSponsor = NULL;

		for (int i = 0; i < strlen(domeniuFirma); i++)
			if (domeniuFirma[i] > 0)
				this->domeniuFirma[i] = domeniuFirma[i];
			else
				this->domeniuFirma[i] = 0;
		this->perioadaSponsorizare = 0;
	}
	Sponsor(const char* numeSponsor, const char domeniuFirma[20], float perioadaSponsorizare)
	{
		if (numeSponsor != NULL)
		{
			this->numeSponsor = new char[strlen(numeSponsor) + 1];
			strcpy(this->numeSponsor, numeSponsor);
		}
		else
			this->numeSponsor = NULL;

		for (int i = 0; i < strlen(domeniuFirma); i++)
			if (domeniuFirma[i] > 0)
				this->domeniuFirma[i] = domeniuFirma[i];
			else
				this->domeniuFirma[i] = 0;

		if (perioadaSponsorizare > 0)
			this->perioadaSponsorizare = perioadaSponsorizare;
		else
			this->perioadaSponsorizare = 0;

	}
	Sponsor(const Sponsor& sp)
	{

		if (sp.numeSponsor != NULL)
		{
			this->numeSponsor = new char[strlen(sp.numeSponsor) + 1];
			strcpy(this->numeSponsor, sp.numeSponsor);
		}
		else
			this->numeSponsor = NULL;

		for (int i = 0; i < strlen(sp.domeniuFirma); i++)
			if (sp.domeniuFirma[i] > 0)
				this->domeniuFirma[i] = sp.domeniuFirma[i];
			else
				this->domeniuFirma[i] = 0;

		if (sp.perioadaSponsorizare > 0)
			this->perioadaSponsorizare = sp.perioadaSponsorizare;
		else
			this->perioadaSponsorizare = 0;
	}
	~Sponsor()
	{
		delete[] this->numeSponsor;
	}
	Sponsor& operator=(const Sponsor& sp)
	{
		delete[]this->numeSponsor;
		if (sp.numeSponsor != NULL)
		{
			this->numeSponsor = new char[strlen(sp.numeSponsor) + 1];
			strcpy(this->numeSponsor, sp.numeSponsor);
		}
		else
			this->numeSponsor = NULL;

		for (int i = 0; i < strlen(sp.domeniuFirma); i++)
			if (sp.domeniuFirma[i] > 0)
				this->domeniuFirma[i] = sp.domeniuFirma[i];
			else
				this->domeniuFirma[i] = 0;

		if (sp.perioadaSponsorizare > 0)
			this->perioadaSponsorizare = sp.perioadaSponsorizare;
		else
			this->perioadaSponsorizare = 0;

		return *this;
	}

	char* getnumeSponsor()
	{
		return this->numeSponsor;
	}
	char* getdomeniuFirma()
	{
		return this->domeniuFirma;
	}
	float getperioadaSponsorizare()
	{
		return this->perioadaSponsorizare;
	}

	void setnumeSponsor(const char* nume)
	{
		if (strlen(nume) > 0)
		{
			if (this->numeSponsor == NULL)
				this->numeSponsor = _strdup(nume);
			else
			{
				delete[]this->numeSponsor;
				this->numeSponsor = _strdup(nume);
			}
		}
		else
			cout << "Nume invalid";
	}

	void setdomeniuFirma(const char* domeniu)
	{
		if (strlen(domeniu) > 0)
		{
			strcpy(this->domeniuFirma, domeniu);
			this->domeniuFirma[strlen(domeniu)] = '\0';

		}
		else
			cout << "Domeniul de activitate nu este corect!" << endl;
	}
	void setperioadaSponsorizare(float h)
	{
		if (h > 0)
			perioadaSponsorizare = h;
		else
			cout << "Perioada de sponsorizare nu este corecta!" << endl;
	}

	//Operatorul index [];
	char operator[](int index) {
		if (this->numeSponsor != NULL)
			return this->numeSponsor[index];
		else
			cout << "Indexul introdus e gresit";
	}
	//Operatorul +
	Sponsor operator+(int sp2)
	{
		this->perioadaSponsorizare = this->perioadaSponsorizare + sp2;
		return *this;
	}
	//Operatorul ++ Forma de preincrementare
	Sponsor operator++(int)
	{
		this->perioadaSponsorizare++;
		return *this;
	}
	//Operatorul ++ Forma de postincrementare
	Sponsor operator++()
	{
		Sponsor cb = *this;
		this->perioadaSponsorizare++;
		return cb;
	}
	//Operator cast
	operator int()
	{
		return this->perioadaSponsorizare;
	}

	//Operator !
	bool operator!()
	{
		if (this->perioadaSponsorizare != 0)
			return true;
		else
			return false;
	}
	//Operator <
	bool operator<(Sponsor& cb)
	{
		if (this->perioadaSponsorizare < cb.perioadaSponsorizare)
			return true;
		else
			return false;
	}
	//Operatorul ==
	bool operator==(const Sponsor& cb)
	{
		if (this->perioadaSponsorizare == cb.perioadaSponsorizare)
			return true;
		else
			return false;
	}
	void writeToFile(fstream& file)
	{

		int lg = strlen(this->numeSponsor) + 1;
		file.write((char*)&lg, sizeof(int));
		file.write(this->numeSponsor, lg);

		int lg2 = strlen(this->domeniuFirma) + 1;
		file.write((char*)&lg2, sizeof(int));
		file.write(this->domeniuFirma, lg2);

		file.write((char*)&this->perioadaSponsorizare, sizeof(float));
	}

	void readFromFile(fstream& file)
	{
		delete[] this->numeSponsor;
		int lg = 0;
		file.read((char*)&lg, sizeof(int));
		this->numeSponsor = new char[lg];
		file.read(this->numeSponsor, lg);

		int lg2 = 0;
		file.read((char*)&lg2, sizeof(int));
		file.read(this->domeniuFirma, lg2);

		file.read((char*)&this->perioadaSponsorizare, sizeof(float));
	}

	friend ostream& operator<<(ostream& out, const Sponsor& cb8);
	friend istream& operator>>(istream& in, Sponsor& cb8);
	friend ofstream& operator<<(ofstream& g, const Sponsor& cb8);
	friend ifstream& operator>>(ifstream& f, Sponsor& cb8);
};
ostream& operator<<(ostream& out, const Sponsor& cb8)
{
	out << "Numele sponsorului: " << cb8.numeSponsor << endl;
	out << "Domeniul activitatii: " << cb8.domeniuFirma << endl;
	out << "Perioada de sponsorizare:  " << cb8.perioadaSponsorizare << endl;
	return out;
}
istream& operator>>(istream& in, Sponsor& cb8)
{
	char numeCb[20];
	if (cb8.numeSponsor != NULL)
		delete[]cb8.numeSponsor;
	cout << "Numele sponsorului: ";
	in >> numeCb;
	cb8.numeSponsor = new char[strlen(numeCb) + 1];
	strcpy(cb8.numeSponsor, numeCb);
	cout << "Domeniu activitate:";
	char domeniu[50];
	in >> domeniu;
	strcpy(cb8.domeniuFirma, domeniu);
	cout << "Perioada sponsorizare: ";
	in >> cb8.perioadaSponsorizare;
	return in;
}
ofstream& operator<<(ofstream& g5, const Sponsor& cb8)
{
	g5 << cb8.numeSponsor << ",";
	for (int i = 0; i < 20; i++)
		g5 << cb8.domeniuFirma[i] << ",";
	g5 << cb8.perioadaSponsorizare << ",";
	return g5;
}
ifstream& operator>>(ifstream& f5, Sponsor& cb8)
{
	delete[]cb8.numeSponsor;
	char numeCb[20];
	f5 >> numeCb;
	cb8.numeSponsor = new char[strlen(numeCb) + 1];
	strcpy(cb8.numeSponsor, numeCb);
	for (int i = 0; i < 20; i++)
		f5 >> cb8.domeniuFirma[i];
	f5 >> cb8.perioadaSponsorizare;
	return f5;

}

void main()
{
	Agentie s1("MRA_Models", "Categoria_A");
	cout << s1 << endl;
	Agentie s2("Models_sc", "Categoria_B", 700.02, 3);
	cout << s2 << endl;
	Agentie s3(s1);
	cout << s3 << endl;
	Agentie s4;
	cin >> s4;
	cout << endl << s4 << endl;
	Agentie s5 = s2;
	cout << s5 << endl;
	s5.setdenumireAgentie("Models_Dinasty");
	cout << s5.getdenumireAgentie() << endl;
	s5.settipAgentie("Categoria_c");
	cout << s5.gettipAgentie() << endl;
	s5.setpretAgentie(50.19);
	cout << s5.getpretAgentie() << endl;
	s5.setdurataContract(5);
	cout << s5.getdurataContract() << endl;
	cout << s1.consultarepretAgentie() << endl;
	int i = 0;
	cout << s1[i] << endl;
	cout << s2 * 4.2f << endl;
	cout << ++s1 << endl;
	cout << s1++ << endl;
	cout << (int)s2 << endl;
	if (!s2)
		cout << "Atributul este diferit de 0";
	else
		cout << "Atributul este egal cu 0";
	cout << endl;
	if (s1 < s2)
		cout << "Atributul din s1 e mai mic ca cel din s2";
	else
		cout << "Atributul din s1 nu e mai mic ca cel din s2";
	cout << endl;
	if (s1 < s2)
		cout << "Preturile agentiilor sunt egale";
	else
		cout << "Preturile agentiilor nu sunt egale";
	cout << endl;

	fstream fOut1("fisier.txt", ios::out | ios::binary);
	s2.writeToFile(fOut1);
	fOut1.close();

	fstream fIn1("fisier.txt", ios::in | ios::binary);
	s1.readFromFile(fIn1);
	fIn1.close();
	cout << s1;
	cout << endl;

	/*ofstream g("Agentii.txt");
	g << s2;
	g.close();*/

	ofstream g("Agentii.csv");
	g << s2;
	g.close();

	ifstream f("Agentii.txt");
	Agentie s20;
	f >> s20;
	cout << s20;
	f.close();


	cout << "\tMeniu agentii" << endl;
	int n, ok = 0;
	while (ok == 0)
	{
		cout << "Pentru a accesa cu agentia s1 tasteaza 1" << endl;
		cout << "Pentru a accesa cu agentia s2 tasteaza 2" << endl;
		cout << "Pentru a iesi din meniu tasteaza 3" << endl;
		cin >> n;
		if (n == 1)
		{
			cout << "Ati selectat agentia " << s1.getdenumireAgentie();
			cout << endl;
			while (n == 1)
			{
				int caz;
				cout << "Pentru a afisa pretul agentiei apasati 1" << endl;
				cout << "Pentru a schimba pretul agentiei apasati 2" << endl;
				cout << "Pentru a afisa durata contractului apasati 3" << endl;
				cout << "Pentru a iesi apasati 4" << endl;
				cin >> caz;
				if (caz == 1)
					cout << "Pretul agentiei din s1 este:" << s1.getpretAgentie();
				cout << endl;
				if (caz == 2)
				{
					float pret_nou;
					cout << "Introduce noul pret: " << endl;
					cin >> pret_nou;
					s1.setpretAgentie(pret_nou);

				}
				if (caz == 3)
					cout << "Durata contractului din s1 este:" << s1.getdurataContract();
				cout << endl;
				if (caz == 4)
					break;

			}

		}

		if (n == 2)
		{
			cout << "Ati selectat agentia: " << s2.getdenumireAgentie();
			cout << endl;
			while (n == 2)
			{
				int caz;
				cout << "Pentru a afisa tipul agentiei apasati 1" << endl;
				cout << "Pentru a schimba durata contractului apasati 2" << endl;
				cout << "Pentru a iesi apasati 3" << endl;
				cin >> caz;
				if (caz == 1)
					cout << "Tipul agentiei s2 este:" << s2.gettipAgentie();
				cout << endl;
				if (caz == 2)
				{
					int durata_noua;
					cout << "Introduce durata noua: " << endl;
					cin >> durata_noua;
					s2.setdurataContract(durata_noua);

				}
				if (caz == 3)
					break;


			}

		}
		if (n == 3)
			break;
	}

	cout << "------------Terminarea clasei Agentie-------------------" << endl << endl;



	Designer d1("Andrei", "Bucuresti");
	cout << d1 << endl;
	Designer d2("Adrian", 30, 2, "Craiova");
	cout << d2 << endl;
	Designer d3(d1);
	cout << d3 << endl;
	Designer d4;
	cin >> d4;
	cout << endl << d4 << endl;
	Designer d5;
	d5.setnumeDesigner("Raluca");
	cout << d5.getnumeDesigner() << endl;
	d5.setvarsta(32);
	cout << d5.getvarsta() << endl;
	d5.setexperienta(12);
	cout << d5.getexperienta() << endl;
	d5.setorasulProvenienta("Sibiu");
	cout << d5.getorasulProvenienta() << endl;
	int j = 0;
	cout << d1[j] << endl;
	cout << d2 / 4 << endl;
	cout << --d2 << endl;
	cout << d2-- << endl;
	cout << (int)d2 << endl;
	if (!d2)
		cout << "Atributul este diferit de 0";
	else
		cout << "Atributul este egal cu 0";
	cout << endl;
	if (d1 > d2)
		cout << "Atributul din d1 nu e mai mic ca cel din d2";
	else
		cout << "Atributul din d1 e mai mic ca cel din d2";
	cout << endl;
	if (d1 > d2)
		cout << "Varstele designerilor nu sunt egale";
	else
		cout << "Varstele designerilor sunt egale";
	cout << endl;

	fstream fOut2("fisier.txt", ios::out | ios::binary);
	d2.writeToFile(fOut2);
	fOut2.close();

	fstream fIn2("fisier.txt", ios::in | ios::binary);
	d1.readFromFile(fIn2);
	fIn2.close();
	cout << d1;
	cout << endl;

	/*ofstream g2("Designers.txt");
	g2 << c2;
	g2.close();*/

	ofstream g2("Designers.csv");
	g2 << d2;
	g2.close();

	ifstream f2("Designers.txt");
	Designer c30;
	f2 >> c30;
	cout << c30;
	f2.close();


	cout << "\tMeniu designers" << endl;
	int n1, ok1 = 0;
	while (ok1 == 0)
	{
		cout << "Pentru a accesa cu designer d1 tasteaza 1" << endl;
		cout << "Pentru a accesa cu designer d2 tasteaza 2" << endl;
		cout << "Pentru a iesi din meniu tasteaza 3" << endl;
		cin >> n1;
		if (n1 == 1)
		{
			cout << "Ati selectat designerul " << d1.getnumeDesigner();
			cout << endl;
			while (n1 == 1)
			{
				int caz1;
				cout << "Pentru a afisa orasul de provenienta apasati 1" << endl;
			
				cout << "Pentru a iesi apasati 4" << endl;
				cin >> caz1;
				if (caz1 == 1)
					cout << "Orasul de provenienta este:" << d1.getorasulProvenienta();
				cout << endl;
				
				if (caz1 == 4)
					break;

			}

		}
		
		if (n1 == 2)
		{
			cout << "Ati selectat agentia: " << d2.getnumeDesigner();
			cout << endl;
			while (n1 == 2)
			{
				int caz2;
				cout << "Pentru a afisa varsta apasati 1" << endl;
				cout << "Pentru a schimba experienta apasati 2" << endl;
				cout << "Pentru a iesi apasati 3" << endl;
				cin >> caz2;
				if (caz2 == 1)
					cout << "Varsta s2 este:" << d2.getvarsta();
				cout << endl;
				if (caz2 == 2)
				{
					int experienta_noua1;
					cout << "Introduce experienta noua: " << endl;
					cin >> experienta_noua1;
					d2.setexperienta(experienta_noua1);

				}
				if (caz2 == 3)
					break;


			}

		}
		if (n1 == 3)
			break;
	}


	cout << "------------Terminarea clasei Designers-------------------" << endl << endl;



	Invitat i1("Tudor", 30);
	cout << i1 << endl;
	Invitat i2("Andreea", 20, 10, 500.99);
	cout << i2 << endl;
	Invitat i3(i1);
	cout << i3 << endl;
	Invitat i4;
	cin >> i4;
	cout << endl << i4 << endl;
	Invitat i5 = i2;
	cout << i5 << endl;
	i5.setnumeInvitat("Alexandru");
	cout << i5.getnumeInvitat() << endl;
	i5.setvarstainvitat(41);
	cout << i5.getvarstaInvitat() << endl;
	i5.setmarime(30);
	cout << i5.getmarime() << endl;
	i5.setsoldBuget(500.70);
	cout << i5.getsoldBuget() << endl;
	cout << i5.consultareSold() << endl;
	int l = 0;
	cout << i1[l] << endl;
	cout << i2 + 2 << endl;
	cout << ++i1 << endl;
	cout << i1++ << endl;
	cout << (int)i2 << endl;
	if (!i2)
		cout << "Atributul este diferit de 0";
	else
		cout << "Atributul este egal cu 0";
	cout << endl;
	if (i1 <= i2)
		cout << "Atributul din c11 e mai mic sau egal ca cel din c12";
	else
		cout << "Atributul din c11 nu e mai mic sau egal ca cel din c12";
	cout << endl;
	if (i1 <= i2)
		cout << "Varstele invitatilor sunt egale";
	else
		cout << "Varstele invitatilor nu sunt egale";
	cout << endl;

	fstream fOut3("fisier.txt", ios::out | ios::binary);
	i2.writeToFile(fOut3);
	fOut3.close();

	fstream fIn3("fisier.txt", ios::in | ios::binary);
	i1.readFromFile(fIn3);
	fIn3.close();
	cout << i1;
	cout << endl;

	/*ofstream g3("Invitat.txt");
	g3 << i2;
	g3.close();*/

	ofstream g3("Invitati.csv");
	g3 << i2;
	g3.close();

	ifstream f3("Invitati.txt");
	Invitat i20;
	f3 >> i20;
	cout << i20;
	f3.close();

	cout << endl << "Relatie de tip has a" << endl;
	locMasa loclamasa(40);
	loclamasa.add_invitat(&i1);
	loclamasa.add_invitat(&i5);
	cout << loclamasa << endl;


	cout << "------------Terminarea clasei invitati-------------------" << endl << endl;



	Articol p1("Fusta", "19.11.2022");
	cout << p1 << endl;

	Articol p2("Tricou", 4567, 100, 250, "10.12.2020");
	cout << p2 << endl;
	Articol p3(p1);
	cout << p3 << endl;
	Articol p4;
	cin >> p4;
	cout << endl << p4 << endl;
	Articol p5 = p2;
	cout << p5 << endl;
	p5.setdenumirearticol("Top");
	cout << p5.getdenumireArticol() << endl;
	p5.setpretarticol(60.00);
	cout << p5.getpretArticol() << endl;
	p5.setcantitate(50);
	cout << p5.getcantitate() << endl;
	p5.setdatafabricatie("15.08.2018");
	cout << p5.getdatafabricatie() << endl;
	int m = 0;
	cout << p1[m] << endl;
	cout << p2 / 24 << endl;
	cout << ++p1 << endl;
	cout << p1++ << endl;
	cout << (int)p2 << endl;
	if (!p2)
		cout << "Atributul este diferit de 0";
	else
		cout << "Atributul este egal cu 0";
	cout << endl;
	if (p1 <= p2)
		cout << "Atributul din p1 e mai mic sau egal ca cel din p2";
	else
		cout << "Atributul din p1 nu e mai mic sau egal ca cel din p2";
	cout << endl;
	if (p1 <= p2)
		cout << "Preturile articolelor sunt egale";
	else
		cout << "Preturile articolelor nu sunt egale";
	cout << endl;

	fstream fOut4("fisier.txt", ios::out | ios::binary);
	p2.writeToFile(fOut4);
	fOut4.close();

	fstream fIn4("fisier.txt", ios::in | ios::binary);
	p1.readFromFile(fIn4);
	fIn4.close();
	cout << p1;
	cout << endl;

	/*ofstream g4("Articole.txt");
	g4 << p2;
	g4.close();*/

	ofstream g4("Articole.csv");
	g4 << p2;
	g4.close();

	ifstream f4("Articole.txt");
	Articol p30;
	f4 >> p30;
	cout << p30;
	f4.close();

	Rochie r1;

	Rochie r2("Fara spate", 5666, 100, 200, "15.08.2020", 3);
	Rochie r3 = r2;
	r1 = r2;
	cout << r1;

	cout << "\nTESTARE METODA CALCUL";
	cout << "\n" << p1.calculpretarticol();
	cout << "\n" << r2.calculpretarticol();

	Pantaloni p11;
	Pantaloni p22("Flare", 233, 200.00, 40, "6.02.2020", 4);
	Pantaloni p33 = p22;
	p11 = p22;
	cout << p11;

	cout << "\nTESTARE METODA CALCUL";
	cout << "\n" << p1.calculpretarticol();
	cout << "\n" << p11.calculpretarticol();


	cout << "------------Terminarea clasei Articol-------------------" << endl << endl;



	Sponsor sp1("Roxana", "Imobiliare");
	cout << sp1 << endl;
	Sponsor sp2("Madalina", "IT", 365);
	cout << sp2 << endl;
	Sponsor sp3(sp1);
	cout << sp3 << endl;
	Sponsor sp4;
	cin >> sp4;
	cout << endl << sp4 << endl;
	Sponsor sp5 = sp2;
	cout << sp5 << endl;
	sp5.setnumeSponsor("Mihai");
	cout << sp5.getnumeSponsor() << endl;
	sp5.setdomeniuFirma("Marketing");
	cout << sp5.getdomeniuFirma() << endl;
	sp5.setperioadaSponsorizare(300);
	cout << sp5.getperioadaSponsorizare() << endl;
	
	cout << sp2 + 6 << endl;
	cout << ++sp1 << endl;
	cout << sp1++ << endl;
	cout << (int)sp2 << endl;
	if (!sp2)
		cout << "Atributul este diferit de 0";
	else
		cout << "Atributul este egal cu 0";
	cout << endl;
	if (sp1 < sp2)
		cout << "Atributul din cb1 e mai mic ca cel din cb2";
	else
		cout << "Atributul din cb1 nu e mai mic ca cel din cb2";
	cout << endl;
	if (sp1 < sp2)
		cout << "Perioadele de sponsorizare sunt egale";
	else
		cout << "Perioadele de sponsorizare nu sunt egale";
	cout << endl;

	fstream fOut5("fisier.txt", ios::out | ios::binary);
	sp2.writeToFile(fOut5);
	fOut5.close();

	fstream fIn5("fisier.txt", ios::in | ios::binary);
	sp1.readFromFile(fIn5);
	fIn5.close();
	cout << sp1;
	cout << endl;

	//ofstream g5("Sponsori.txt");
	//g5 << cb2;
	//g5.close();

	ofstream g5("Sponsori.csv");
	g5 << sp2;
	g5.close();

	ifstream f5("Sponsor.txt");
	Sponsor cb20;
	f5 >> cb20;
	cout << cb20;
	f5.close();

	cout << "------------Terminarea clasei Sponsor-------------------" << endl << endl;

	//STL VECTOR
	cout << "\n----------------STL VECTOR-------------------\n";
	vector<Agentie> vSt;
	vSt.push_back(s1);
	vSt.push_back(s5);

	vector<Agentie>::iterator itV2;
	for (itV2 = vSt.begin(); itV2 != vSt.end(); itV2++)
		cout << *itV2;

	//STL LIST
	cout << "\n----------------STL LIST-------------------\n";
	list<Agentie> lSt;
	lSt.push_back(s1);
	lSt.push_front(s5);

	list<Agentie>::iterator itLEv;
	for (itLEv = lSt.begin(); itLEv != lSt.end(); itLEv++)
		cout << *itLEv << " ";

	////STL SET
	// cout << "\n----------------STL SET-------------------\n";
	//set<Clienti> setClienti;
	//setClienti.insert(cl1);
	//setClienti.insert(cl2);
	//setClienti.insert(cl1);

	//set<Clienti>::iterator itSCl;
	//for (itSCl = setClienti.begin(); itSCl != setClienti.end(); itSCl++)
	//	cout << *itSCl;

	//STL MAP
	/*cout << "\n----------------STL MAP-------------------\n";
	map<int, Agentie> mapAgentie;
	mapAgentie[0] = s1;
	mapAgentie[4] = s2;
	mapAgentie[10] = s2;
	mapAgentie[0] = s3;

	map<int, Agentie>::iterator itMap;
	for (itMap = mapAgentie.begin(); itMap != mapAgentie.end(); itMap++)
		cout << itMap->first << " " << itMap->second << endl;*/



}
