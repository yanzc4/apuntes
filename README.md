# APUNTES
12-09-2023
<hr>

## para login
- se agrega en el evento click del boton

            String nombre,pass,user;
            nombre = ddlCategoria.SelectedValue;
            user = txtUsuario.Text;
            pass = txtPass.Text;

            if (user == "argentina" && pass == "123")
            {
                Response.Redirect("paginainicio.aspx?nom=" + nombre);
            }
            else
            {
                //Response.Write("Credenciales incorrectas");
                string script = @"<script type='text/javascript'>
                            alert('credenciales incorrectas');
                        </script>";

                ScriptManager.RegisterStartupScript(this, typeof(Page), "alerta", script, false);
            }
## para recuperar las variables desde la url
- se agrega al evento load page
  
            string nombre;
            nombre = Request.QueryString["nom"];
            lblSaludo.Text = "Hola " + nombre;

## sesion por url
- creamos la variable de sesion desde la pagina de login

            String nombre,pass,user;
            nombre = ddlCategoria.SelectedValue;
            user = txtUsuario.Text;
            pass = txtPass.Text;

            if (user == "argentina" && pass == "123")
            {
              //sesion
                Session["usuario"] = user;
                Response.Redirect("paginainicio.aspx?nom=" + nombre);
            }
            else
            {
                //Response.Write("Credenciales incorrectas");
                string script = @"<script type='text/javascript'>
                            alert('credenciales incorrectas');
                        </script>";

                ScriptManager.RegisterStartupScript(this, typeof(Page), "alerta", script, false);
            }

 - capturamos la variable de sesion (load)

            string nombre, user;
            nombre = Request.QueryString["nom"];
            user = Session["usuario"] as string;

            lblSaludo.Text = "Hola " + nombre;
            lblUsuario.Text = user;

## para pasar valores de un lixbox

[![image.png](https://i.postimg.cc/rFQLFTqf/image.png)](https://postimg.cc/fJtPB6td)

        protected void Button1_Click1(object sender, EventArgs e)
        {
            ListBox1.Items.Add(txtAgregar.Text);
            txtAgregar.Text = "";
        }

        protected void Button4_Click(object sender, EventArgs e)
        {
            ListBox2.Items.Add(ListBox1.SelectedValue);
            ListBox1.Items.Remove(ListBox1.SelectedValue);
        }

        protected void Button5_Click(object sender, EventArgs e)
        {
            ListBox1.Items.Add(ListBox2.SelectedValue);
            ListBox2.Items.Remove(ListBox2.SelectedValue);
        }

        protected void Button3_Click(object sender, EventArgs e)
        {
            for (int i = 0; i <= ListBox1.Items.Count - 1; i++)
            {
                ListBox2.Items.Add(ListBox1.Items[i].ToString());
            }
            ListBox1.Items.Clear();
        }

        protected void Button2_Click(object sender, EventArgs e)
        {
            for (int i = 0; i <= ListBox2.Items.Count - 1; i++)
            {
                ListBox1.Items.Add(ListBox2.Items[i].ToString());
            }
            ListBox2.Items.Clear();
        }

## para crear tipo factura

[![image.png](https://i.postimg.cc/W4m8TNv3/image.png)](https://postimg.cc/3yRmZHW5)

        protected void dplProductos_SelectedIndexChanged(object sender, EventArgs e)
        {
            txtPrecio.Text = dplProductos.SelectedValue;
        }

        protected void btnAgregar_Click(object sender, EventArgs e)
        {
            try
            {
                double precio, subtotal, acumulador;
                acumulador = 0;
                int cant;
                String nombre;
                precio = double.Parse(txtPrecio.Text);
                cant = int.Parse(txtCantidad.Text);
                nombre = dplProductos.SelectedItem.Text;

                subtotal = precio * cant;

                lbxProductos.Items.Add(nombre);
                lbxPrecio.Items.Add(precio.ToString());
                lbxCantidad.Items.Add(cant.ToString());
                lbxSubotal.Items.Add(subtotal.ToString());

                for (int i = 0; i <= lbxSubotal.Items.Count - 1; i++)
                {
                    acumulador = acumulador + double.Parse(lbxSubotal.Items[i].ToString());
                }
                lblTotal.Text = acumulador.ToString();
                txtCantidad.Text = "";
                lblError.Text = "";
            }
            catch
            {
                //lblError.Text = "Ah ocurrido un error no debe haber campos vacios";
                string script = @"<script type='text/javascript'>
                            alerta();
                        </script>";

                ScriptManager.RegisterStartupScript(this, typeof(Page), "alerta", script, false);
            }
        }

        protected void btnEliminar_Click(object sender, EventArgs e)
        {
            lbxCantidad.Items.Clear();
            lbxPrecio.Items.Clear();
            lbxProductos.Items.Clear();
            lbxSubotal.Items.Clear();
            lblTotal.Text = "";
            txtCantidad.Text = "";
            txtPrecio.Text = "";
        }

        protected void btnEliminaSeleccion_Click(object sender, EventArgs e)
        {
            int indexlbx;
            double acumulador = 0;

            indexlbx = lbxProductos.SelectedIndex;
            if(indexlbx >= 0 && indexlbx < lbxProductos.Items.Count)
            {
                lbxCantidad.Items.RemoveAt(indexlbx);
                lbxPrecio.Items.RemoveAt(indexlbx);
                lbxProductos.Items.RemoveAt(indexlbx);
                lbxSubotal.Items.RemoveAt(indexlbx);
            }
            for (int i = 0; i <= lbxSubotal.Items.Count - 1; i++)
            {
                acumulador = acumulador + double.Parse(lbxSubotal.Items[i].ToString());
            }
            lblTotal.Text = acumulador.ToString();
        }
- el dropdownList debe activarse el autoPostBack

  [![image.png](https://i.postimg.cc/D0GdpnBn/image.png)](https://postimg.cc/2LzZVpsK)
        
