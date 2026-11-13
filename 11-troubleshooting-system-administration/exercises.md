# លំហាត់មេរៀនទី ១១៖ Troubleshooting និង System Administration

## Scenario

អ្នកប្រើរាយការណ៍ថា website មួយមិនឆ្លើយតប។ អ្នកមានសិទ្ធិអានស្ថានភាព server ប៉ុណ្ណោះ ហើយមិនទាន់បានអនុម័តឱ្យ restart ឬកែ configuration។

## កិច្ចការ

1. កត់ symptom, start time និង impact។
2. ពិនិត្យ uptime, memory, disk និង process list។
3. ប្រសិនបើមាន systemd ពិនិត្យ service status និង journal។
4. ពិនិត្យ listening sockets និង network route/DNS តាមតម្រូវការ។
5. សម្គាល់ facts ពី hypotheses។
6. បំពេញ incident notes ដោយដក secrets/identifiers ចេញ។
7. សរសេរថាតើ change ណាដែលអ្នកស្នើ និង rollback plan អ្វី—but កុំអនុវត្ត change ក្នុងលំហាត់នេះ។

## សំណួរពិចារណា

- តើ evidence ណាដែលបង្ហាញថាបញ្ហានៅ application, host ឬ network?
- តើអ្វីនៅមិនទាន់ដឹង?
- តើនរណាត្រូវអនុម័ត change?
- តើអ្នកនឹងវាស់វែងជោគជ័យក្រោយ change ដូចម្តេច?

## លក្ខខណ្ឌបញ្ចប់

- មាន read-only evidence និងពេលវេលាច្បាស់។
- មិនបង្ហាញ sensitive logs។
- Change និង rollback ត្រូវបានសរសេរ មិនអនុវត្តដោយគ្មានអនុម័ត។
