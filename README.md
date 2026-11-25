# سکته قلبی را بشناسیم

A Persian (RTL) educational website about heart attacks: symptoms, emergency steps, a CPR rhythm trainer, a risk-factor checklist, myths vs. facts and a short quiz.

Made by **یاسمن آژیر** and **مائده خبازکار**.

## Files

```
index.html                    the whole website (HTML + CSS + JS in one file)
fonts/                        Vazirmatn font, self-hosted (no Google Fonts needed)
docs/project-report.pdf       project report for the teacher
docs/presentation-guide.pdf   presentation preparation guide
```

It is a static site with no build step, no backend and no dependencies. Any web server can host it.

## Deploy on your server (nginx)

```bash
# 1. Get the files onto the server
sudo git clone https://github.com/RootedMani/heart-attack-website.git /var/www/heart
```

```nginx
# 2. /etc/nginx/sites-available/heart
server {
    listen 80;
    server_name example.com www.example.com;   # your domain
    root /var/www/heart;
    index index.html;

    location ~ /\.git { deny all; }
    location /fonts/ { expires 30d; add_header Cache-Control "public"; }
}
```

```bash
# 3. Enable it and add HTTPS
sudo ln -s /etc/nginx/sites-available/heart /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
sudo certbot --nginx -d example.com -d www.example.com
```

Point your domain's DNS `A` record at the server's IP before running certbot.

To update later: `cd /var/www/heart && sudo git pull`

## Test locally

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Notes

- The CPR button's sound only plays after a click (browser rule), so it works on a real page.
- The fonts are self-hosted, so the site loads even where Google Fonts is blocked or slow.
- Font: [Vazirmatn](https://github.com/rastikerdar/vazirmatn), SIL Open Font License (`fonts/OFL-LICENSE.txt`).
- This website is for education only and does not replace medical advice.
