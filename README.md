using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsAppVideojuego3
{
    public partial class Form2 : Form
    {
        public Form2()
        {
            InitializeComponent();
        }
        int velocidad = 5;
        int contador = 0; //Cuenta el puntaje para aumentar la velocidad
        int puntaje = 0;

        bool arribabajo;
        bool izquierdadere;

        private void Form2_Load(object sender, EventArgs e)
        {
            this.Text = "Puntaje: 0";
            Random Mix = new Random();
            pictureBox1.Location = new Point(0, Mix.Next(this.Height));
            arribabajo = true;
            izquierdadere = true;
            timer1.Enabled = true;
            puntaje = 0;
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            if (pictureBox1.Left > pictureBox2.Left) //cuando se va la pelota
            {
                timer1.Enabled = false;
                MessageBox.Show("Tu puntaje es:" + puntaje.ToString() + " punto(s)");
                puntaje = 0;
                velocidad = 5;
                contador = 0;
            }

            //rebote
            if (pictureBox1.Left + pictureBox1.Width >= pictureBox2.Left &&//que este dentro del rango
                pictureBox1.Left + pictureBox1.Width <= pictureBox2.Left + pictureBox2.Width && //checa que no pase de la posición de la imagen2
                pictureBox1.Top + pictureBox1.Height >= pictureBox2.Top &&//imagen1 no puede estar más arriba de la imagen2
                pictureBox1.Top + pictureBox1.Height <= pictureBox2.Top + pictureBox2.Height)//que no se vaya para abajo
            { 
                izquierdadere=false;
                puntaje += 1;
                this.Text = "Puntaje hasta ahora:" + puntaje.ToString() + "";
                contador += 1;
                if (contador>5)
                {
                    velocidad += 1;
                    contador = 0;
                }
            }

            #region
            if (izquierdadere) //movimiento pelota de unlado a otro
            {
                pictureBox1.Left += velocidad;
            }
            else
            {
                pictureBox1.Left -= velocidad;
            }

            if (arribabajo) //movimiento de arriba a bajo
            {
                pictureBox1.Top += velocidad;
            }
            else
            {
                pictureBox1.Top -= velocidad;
            }

            if (pictureBox1.Top >= this.Height - 50) //pared de abajo
            {
                arribabajo = false;
            }

            if (pictureBox1.Top <= 0) //pared de arriba
            {
                arribabajo = true;
            }
            if (pictureBox1.Left <= 0)
            {
                izquierdadere = true;
            }
            #endregion



        }


        private void Form2_MouseMove(object sender, MouseEventArgs e)
        {
            pictureBox2.Top=e.Y;//Mover la raqueta
        }

        private void pictureBox1_Click(object sender, EventArgs e)
        {
            
        }

        private void pictureBox1_Paint(object sender, PaintEventArgs e)
        {
            
        }
    }
}
