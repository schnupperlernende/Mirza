# Mirza
git add .
git commit -m "Deine Commit Nachricht"
git branch -M main
git remote add origin git@github.com:schnupperlernende/Mirza.git
git push -u origin main
Zuerst muss man sich über der SSH auf den Raspberey Pi verbinden und gibt den folgenden Befehl für den Terminal ein: ssh ubuntu@IP-Adresse
Als man sich mit dem Raspberry verbunden hat, muss man danach ein Nginx installieren mit dem Befehl: sudo apt update. Danach grad noch den Befehl: sudo apt install nginx.
Als nächsten Schritt erstellt man eine Firewall mit dem Befehl: sudo ufw app list. Anschliessend kontrolliert man ob man das auf diesem Bildschrim zu sehen ist: Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
  Danach aktiviert man den Nginx HTTP mit dem Befehl: sudo ufw allow 'Nginx HTTP'. Anschliessend verifiziert man es mit: sudo ufw status.
  Man konntrolliert den Web Server mit: systemctl status nginx.
  Um zu schauen ob der Server aktiv ist, gibt man diesen Code ein: http://your_server_ip.
  Um eine Datei zu erstellen gibt man diese Befehle ein:
  sudo mkdir -p /var/www/your_domain/html
  sudo chown -R $USER:$USER /var/www/your_domain/html
  sudo chmod -R 755 /var/www/your_domain
  sudo nano /var/www/your_domain/html/index.html
  In dieser Datei fügt man diesen Text hinzu.
  <html>
    <head>
        <title>Welcome to your_domain!</title>
    </head>
    <body>
        <h1>Success!  The your_domain server block is working!</h1>
    </body>
</html>
Und bestätigt es mit Ctrl+X
Im nächsten Schritt erstellt man eine neue Datei mit dem Befehl: sudo nano /etc/nginx/sites-available/your_domain
Anschliessend kann man wieder diesen Text in der Datei hinzufügen
server {
        listen 80;
        listen [::]:80;

        root /var/www/your_domain/html;
        index index.html index.htm index.nginx-debian.html;

        server_name your_domain www.your_domain;

        location / {
                try_files $uri $uri/ =404;
        }
}
Im nächsten Schritt schaltete ich mehrere Server Blöcke auf mit den Befehlen:
