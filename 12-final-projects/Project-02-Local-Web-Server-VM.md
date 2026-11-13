# Final Project 02: Local Web Server ក្នុង VM

## គោលដៅ

ដំឡើង និងដំណើរការ web service សាកល្បងក្នុង Ubuntu/Debian VM ដែលបំបែកពី production។ អ្នកនឹងអនុវត្ត package management, services, logs, networking, file permissions និង backup។

## តម្រូវការ

- ប្រើ VM ឬ lab machine ដែលអ្នកគ្រប់គ្រង។
- ដំឡើង web server package ពី official repository។
- ចាប់ផ្ដើម service តាម systemd ប្រសិនបើប្រើ។
- ដាក់ static test page ក្នុង document root ដែលសមស្រប។
- កំណត់ ownership/permissions ដោយ least privilege។
- ពិនិត្យ service status, listening port និង logs។
- សាក request ពី VM ឬ host network តាមរបៀបដែលអ្នកបានអនុញ្ញាត។
- Backup configuration និង test page ហើយកត់ restore steps។

កុំបើក service ទៅ public Internet ក្នុង project នេះ។ ប្រើ VM isolated/NAT ឬ private lab network។ កុំបិទ firewall; ប្រសិនបើត្រូវការកែ network access សូមប្រើ sandbox និងសិទ្ធិដែលអ្នកគ្រប់គ្រង។

## ដំណាក់កាល

1. កត់ distro/version និង network mode។
2. ដំឡើង package និងកត់ version។
3. ពិនិត្យ service state និង logs។
4. ដាក់ test page និងផ្ទៀងផ្ទាត់ permission។
5. ពិនិត្យ listening sockets និងសាក HTTP request។
6. បង្កើត backup ហើយសាក restore ទៅទីតាំងសាកល្បង។
7. កត់ troubleshooting notes និងចំណុចដែលត្រូវធ្វើមុន production។

## Deliverables

- Network/service diagram សង្ខេប។
- Install/configuration steps ដែលអាចធ្វើឡើងវិញ។
- Output សម្រាប់ status/log/port checks ដោយលាក់ sensitive data។
- Backup និង restore evidence។
- Security checklist និងចំណុចខ្វះខាតដែលមិនទាន់ដោះស្រាយ។

## Rubric

- Service ដំណើរការក្នុង lab ដោយមានសិទ្ធិត្រឹមត្រូវ: 25%
- Permissions និង network boundary: 20%
- Logs/monitoring និង troubleshooting: 20%
- Backup/restore: 20%
- Documentation និង repeatability: 15%
