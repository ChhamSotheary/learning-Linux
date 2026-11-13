# មេរៀនទី ៧៖ Container Security និង Image Hygiene

## Container មិនមែនជា sandbox ដោយស្វ័យប្រវត្តិ

Container runtime ប្រើ kernel features ដើម្បីផ្តល់ filesystem view, process/network isolation និង resource controls។ Container នៅតែចែករំលែក kernel របស់ host។ កំហុស runtime, privileged mode, mount ដែលបើកទូលាយ ឬ capability លើសតម្រូវការ អាចបង្កើនផលប៉ះពាល់ដល់ host។

## Checklist សម្រាប់ការរចនាសុវត្ថិភាព

- ប្រើ rootless mode ប្រសិនបើសមស្រប និងគាំទ្រ។
- កំណត់ user មិនមែន root ក្នុង image នៅពេលអាចធ្វើបាន។
- កុំប្រើ privileged mode ដោយគ្មានហេតុផល និងការវាយតម្លៃ។
- ដក Linux capabilities ដែលមិនចាំបាច់។
- រក្សា seccomp និង LSM policy បើក។
- កំណត់ CPU, memory និង PID limits សមស្រប។
- កុំ mount Docker/container runtime socket ទៅក្នុង container ដោយមិនយល់ពីសិទ្ធិដែលវាផ្តល់។
- ប្រើ image តូចពីប្រភពជឿទុកចិត្ត, pin digest, ស្កេន vulnerability និងកំណត់ provenance។
- បំបែក secret ចេញពី image layer និង source control; ផ្តល់ secret តាម secret manager/runtime។

ឧទាហរណ៍នេះគ្រាន់តែបង្ហាញគំនិត Dockerfile; ត្រូវសាកល្បងក្នុង project របស់ខ្លួន៖

~~~dockerfile
FROM php:8.3-cli
WORKDIR /app
COPY --chown=www-data:www-data . /app
USER www-data
CMD ["php", "app.php"]
~~~

Version tag មួយអាចត្រូវបានប្ដូរតាមពេលវេលា; សម្រាប់ការបង្កើតដដែលៗ ត្រូវជ្រើស version ដែលគម្រោងគាំទ្រ និងពិចារណា pin image digest តាម workflow របស់អ្នក។ កុំយក Dockerfile ឧទាហរណ៍នេះទៅ production ដោយមិនពិនិត្យ base image, user, file permissions និង runtime needs។

## លំហាត់រចនា

សរសេរ threat model តូចមួយសម្រាប់ web app container៖
1. តើអ្វីជាអ្វីដែលត្រូវការពារ?
2. ប្រសិនបើ app ត្រូវបានគ្រប់គ្រងដោយ attacker តើវាអាចចូលដល់អ្វី?
3. តើអ្នកនឹងកាត់បន្ថយ filesystem, network, capabilities និង resource access ដូចម្តេច?
4. តើអ្នកនឹងទទួលបាន image update និង secret ដោយសុវត្ថិភាពយ៉ាងដូចម្តេច?

## ឯកសារយោង

- [Namespaces manual](https://man7.org/linux/man-pages/man7/namespaces.7.html)
- [Capabilities manual](https://man7.org/linux/man-pages/man7/capabilities.7.html)
- [Kernel cgroup v2 documentation](https://docs.kernel.org/admin-guide/cgroup-v2.html)
