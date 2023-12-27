# BibliotecaPae
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Scaffale
    {
        public string Numero {  get; set; }
        
        public Scaffale(string Numero)
        {
            this.Numero = Numero;
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Program
    {
        static void Main(string[] args)
        {
            //int a = 5;
            Persona p= new Persona("Marco", "Rossi");
            Documento d = new Documento("A1", "Lo Strazio", 1996, "Horror");
            Documento d2 = new Documento("A2", "L'Abominio", 2004, "Commedia");
            Documento d3 = new Documento("A3", "La gag", 2022, "Commedia");
            Persona p2 = new Persona("Francesco", "Marchi");
            Persona p3 = new Persona("Luigi", "Capuato");
            Prestito pe = new Prestito("T1", new DateTime(2016, 3, 28), new DateTime(2016, 4, 28), p3, d);
            d.ImpostainPrestito();
            Prestito pe2 = new Prestito("T2", new DateTime(2023, 12, 20), new DateTime(2024, 1, 20), p, d2);
            d2.ImpostainPrestito();

            Documento[] ad = new Documento[3];
            ad[0] = d;
            ad[1] = d2;
            ad[2] = d3;

            Prestito[] pb = new Prestito[2];
            pb[0] = pe;
            pb[1] = pe2;

            Persona[] u = new Persona[3];
            u[0] = p;
            u[1] = p2;
            u[2] = p3;

            Biblioteca b = new Biblioteca("Bibliote comunale", ad, pb, u);

            Console.WriteLine("Inserisci cosice: ");
            string Codice = Console.ReadLine();
            Documento risultato = b.CercaCodice(Codice);
            Console.WriteLine("{0}", risultato);
           

            Console.WriteLine("Inserisci titolo: ");
            string Titolo = Console.ReadLine();
            Documento t = b.CercaTitolo(Titolo);
            Console.WriteLine("{0}", t);
            Console.ReadLine();
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Prestito
    {
        public string Numero {  get; set; }
        public DateTime Dal { get; set; }
        public DateTime Al {  get; set; }
        public Documento documento { get; set; }
        public Persona persona { get; set; }
        
        public Prestito(string Numero, DateTime Dal, DateTime al, Persona persona, Documento documento)
        {
            this.Numero = Numero;
            this.Dal = Dal; 
            this.Al = al;
            this.persona = persona;
            this.documento = documento;
        }

        public override string ToString()
        {
            return String.Format("{0}, {1}, {2}", Numero, Dal, Al);
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Persona
    {
        public string Nome { get; set; }
        public string Cognome { get; set; }

        public override string ToString()
        {
            return String.Format("{0} {1}", Nome, Cognome);
        }

        public Persona(string Nome, string Cognome)
        {
            this.Nome = Nome;
            this.Cognome = Cognome;
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Libro : Documento
    {
        public int NumeroPagine { get; set; }
        public Libro(int numeroPagine, string Codice, string Titolo, int Anno, string Settore) : base(Codice, Titolo, Anno, Settore)
        {
            this.NumeroPagine = numeroPagine;
        }

        public override string ToString()
        {
            return "";
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class DVD : Documento
    {
        public int Durata {  get; set; }

        public DVD(int Durata, string Codice, string Titolo, int Anno, string Settore) : base(Codice, Titolo, Anno, Settore)
        { 
            this.Durata = Durata;
        }

        public override string ToString()
        {
            return "";
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{

    internal class Documento
    {
        public enum Stato
        {
            InPrestito,
            Disponibile
        }

        public string Codice { get; set; }
        public string Titolo { get; set; }
        public int Anno { get; set; }
        public string Settore { get; set; }
        public Stato Statodoc { get; set; }
        public Scaffale scaffale { get; set; }
        public List<Autore> Autori { get; set; }

        public Documento(string Codice, string Titolo, int Anno, string Settore)
        {
            this.Codice = Codice;
            this.Titolo = Titolo;
            this.Anno = Anno;
            this.Settore = Settore;
            this.Statodoc = Stato.Disponibile;
        }

        public override string ToString() 
        {
            return string.Format("il codice del documento è {0}; il suo titolo è {1}, l'anno di pubblicazione è {2}, il suo settore è {3}, lo stato del documento è{4}",
            Codice, Titolo, Anno, Settore, Statodoc); 
        }
        
        public void ImpostainPrestito()
        {
            Statodoc = Stato.InPrestito;
          
        }

        public void ImpostaDisponibile()
        {
            Statodoc = Stato.Disponibile;
        }


    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{

    internal class Documento
    {
        public enum Stato
        {
            InPrestito,
            Disponibile
        }

        public string Codice { get; set; }
        public string Titolo { get; set; }
        public int Anno { get; set; }
        public string Settore { get; set; }
        public Stato Statodoc { get; set; }
        public Scaffale scaffale { get; set; }
        public List<Autore> Autori { get; set; }

        public Documento(string Codice, string Titolo, int Anno, string Settore)
        {
            this.Codice = Codice;
            this.Titolo = Titolo;
            this.Anno = Anno;
            this.Settore = Settore;
            this.Statodoc = Stato.Disponibile;
        }

        public override string ToString() 
        {
            return string.Format("il codice del documento è {0}; il suo titolo è {1}, l'anno di pubblicazione è {2}, il suo settore è {3}, lo stato del documento è{4}",
            Codice, Titolo, Anno, Settore, Statodoc); 
        }
        
        public void ImpostainPrestito()
        {
            Statodoc = Stato.InPrestito;
          
        }

        public void ImpostaDisponibile()
        {
            Statodoc = Stato.Disponibile;
        }


    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{

    internal class Documento
    {
        public enum Stato
        {
            InPrestito,
            Disponibile
        }

        public string Codice { get; set; }
        public string Titolo { get; set; }
        public int Anno { get; set; }
        public string Settore { get; set; }
        public Stato Statodoc { get; set; }
        public Scaffale scaffale { get; set; }
        public List<Autore> Autori { get; set; }

        public Documento(string Codice, string Titolo, int Anno, string Settore)
        {
            this.Codice = Codice;
            this.Titolo = Titolo;
            this.Anno = Anno;
            this.Settore = Settore;
            this.Statodoc = Stato.Disponibile;
        }

        public override string ToString() 
        {
            return string.Format("il codice del documento è {0}; il suo titolo è {1}, l'anno di pubblicazione è {2}, il suo settore è {3}, lo stato del documento è{4}",
            Codice, Titolo, Anno, Settore, Statodoc); 
        }
        
        public void ImpostainPrestito()
        {
            Statodoc = Stato.InPrestito;
          
        }

        public void ImpostaDisponibile()
        {
            Statodoc = Stato.Disponibile;
        }


    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{

    internal class Documento
    {
        public enum Stato
        {
            InPrestito,
            Disponibile
        }

        public string Codice { get; set; }
        public string Titolo { get; set; }
        public int Anno { get; set; }
        public string Settore { get; set; }
        public Stato Statodoc { get; set; }
        public Scaffale scaffale { get; set; }
        public List<Autore> Autori { get; set; }

        public Documento(string Codice, string Titolo, int Anno, string Settore)
        {
            this.Codice = Codice;
            this.Titolo = Titolo;
            this.Anno = Anno;
            this.Settore = Settore;
            this.Statodoc = Stato.Disponibile;
        }

        public override string ToString() 
        {
            return string.Format("il codice del documento è {0}; il suo titolo è {1}, l'anno di pubblicazione è {2}, il suo settore è {3}, lo stato del documento è{4}",
            Codice, Titolo, Anno, Settore, Statodoc); 
        }
        
        public void ImpostainPrestito()
        {
            Statodoc = Stato.InPrestito;
          
        }

        public void ImpostaDisponibile()
        {
            Statodoc = Stato.Disponibile;
        }


    }
}
0using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{

    internal class Documento
    {
        public enum Stato
        {
            InPrestito,
            Disponibile
        }

        public string Codice { get; set; }
        public string Titolo { get; set; }
        public int Anno { get; set; }
        public string Settore { get; set; }
        public Stato Statodoc { get; set; }
        public Scaffale scaffale { get; set; }
        public List<Autore> Autori { get; set; }

        public Documento(string Codice, string Titolo, int Anno, string Settore)
        {
            this.Codice = Codice;
            this.Titolo = Titolo;
            this.Anno = Anno;
            this.Settore = Settore;
            this.Statodoc = Stato.Disponibile;
        }

        public override string ToString() 
        {
            return string.Format("il codice del documento è {0}; il suo titolo è {1}, l'anno di pubblicazione è {2}, il suo settore è {3}, lo stato del documento è{4}",
            Codice, Titolo, Anno, Settore, Statodoc); 
        }
        
        public void ImpostainPrestito()
        {
            Statodoc = Stato.InPrestito;
          
        }

        public void ImpostaDisponibile()
        {
            Statodoc = Stato.Disponibile;
        }


    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Biblioteca
    {
        public string Nome { get; set; }
        public Documento[] Documenti { get; set; } 
        public Prestito[] Prestiti { get; set; }
        public Persona[] Persone { get; set; }


        public Biblioteca(string Nome, Documento[] Documenti, Prestito[] Prestiti, Persona[] Persone)
        {
            this.Nome = Nome;
            this.Documenti = Documenti;
            this.Prestiti = Prestiti;
            this.Persone = Persone;
        }
        
        public Documento CercaCodice(string Codice)
        {
            for(int i = 0; i< Documenti.Length; i++)
            {
                if (Documenti[i].Codice == Codice)
                {
                    return Documenti[i];
                }
            }

            return null;
        }

        public Documento CercaTitolo(string Titolo) 
        {
            for(int i = 0; i< Documenti.Length; i++)
            {
                if (Documenti[i].Titolo == Titolo)
                {
                    return Documenti[i];
                }
            }

            return null;
        
        }

        public Prestito CercaPrestito(string Numero)
        {
            for(int i = 0;i< Prestiti.Length; i++)
            {
                if (Prestiti[i].Numero == Numero)
                {
                    return Prestiti[i];
                }
            }

            return null;
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp12
{
    internal class Autore : Persona
    {
        public Autore(string Nome, string Cognome) : base(Nome, Cognome)
        {
            this.Nome = Nome;
            this.Cognome = Cognome;
        }
    }
}






