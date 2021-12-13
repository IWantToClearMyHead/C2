### Meson
There are many build system, i.e. make, cmake, ant, maven, gradle, and etc, here we are going to learn meson, due to the trend.

```
# ls
a.c  builddir  meson.build
# cat a.c
#include <gtk/gtk.h>

//
// Should provided the active view for a GTK application
//
static void activate(GtkApplication* app, gpointer user_data)
{
  GtkWidget *window;
  GtkWidget *label;

  window = gtk_application_window_new (app);
  label = gtk_label_new("Hello Meson");
  gtk_container_add (GTK_CONTAINER (window), label);
  gtk_window_set_title(GTK_WINDOW (window), "Welcome to Meson");
  gtk_window_set_default_size(GTK_WINDOW (window), 200, 100);
  gtk_widget_show_all(window);
} // end of function activate

//
// main is where all program execution starts
//
int main(int argc, char **argv)
{
  GtkApplication *app;
  int status;

  app = gtk_application_new(NULL, G_APPLICATION_FLAGS_NONE);
  g_signal_connect(app, "activate", G_CALLBACK(activate), NULL);
  status = g_application_run(G_APPLICATION(app), argc, argv);
  g_object_unref(app);

  return status;
}
# cat meson.build 
project('a', 'c')
gtkdep = dependency('gtk+-3.0')
executable('a', 'a.c', dependencies : gtkdep)
# /usr/local/bin/meson setup builddir
# /usr/local/bin/meson compile (or) cd builddir; ninja
```

### Build
<a href="#top">Back to top</a>
