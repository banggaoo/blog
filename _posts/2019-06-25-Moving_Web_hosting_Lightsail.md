---
title: "Moving Web hosting server to Lightsail"
date: 2019-06-25
---

For shifting old-fashioned web hosting server to new one, i decide to use AWS’s Lightsail.

1. Download all data from current web server using FTP.
2. Export WordPress data using exporter plug-in.
3. Create AWS Account for web hosting management.
4. Create IAM Account for same.
5. Create Lightsail instance. Install WordPress app.
6. Make Static IP.
7. Download SSH Key.
8. Connect SSH, SFTP, HTPP for testing.
9. Enter WordPress console.
10. Import WordPress data exported before.
11. 'scp' data to htdocs folder.
12. Remove bitnami flag and restart apache
13. Make snapshot.
14. Create DNS zone.
15. Create A record and resolves to static ip.
16. Configure dns server data in DNS management service.

Create Lightsail instance is easy, but WordPress migration is failed everytime. So i have to manually migrate some datas.
