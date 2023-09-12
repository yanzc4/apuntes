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
