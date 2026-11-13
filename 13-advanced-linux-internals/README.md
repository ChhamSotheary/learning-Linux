# ម៉ូឌុលទី ១៣៖ Linux Internals កម្រិតខ្ពស់

ម៉ូឌុលនេះរៀបរាប់ពីផ្នែកខាងក្នុងដែលមេរៀនមូលដ្ឋានជាច្រើនរំលង៖ process ទាក់ទង kernel យ៉ាងដូចម្តេច, container ពឹងលើ namespaces និង cgroups យ៉ាងណា, systemd គ្រប់គ្រង dependency, និងរបៀបស្វែងរកមូលហេតុ performance ឬបញ្ហាសុវត្ថិភាព។

## លំដាប់មេរៀន

1. [ពី Process ទៅ System Call](lesson-01-processes-and-system-calls.md)
2. [Namespaces និង Cgroups៖ គ្រឹះរបស់ Container](lesson-02-namespaces-and-cgroups.md)
3. [Systemd៖ Dependencies និង Startup Order](lesson-03-systemd-dependencies.md)
4. [Performance Observability និង eBPF](lesson-04-performance-observability.md)
5. [Memory Pressure, Page Cache និង OOM](lesson-05-memory-pressure.md)
6. [Capabilities, Seccomp និង LSM](lesson-06-linux-security-boundaries.md)
7. [Container Security និង Image Hygiene](lesson-07-container-security.md)
8. [លំហាត់ និង Lab សរុប](exercises.md)

## របៀបរៀន

ប្រើ VM ឬម៉ាស៊ីនសាកល្បងដែលអ្នកគ្រប់គ្រង។ ចាប់ផ្តើមដោយ command សម្រាប់អានព័ត៌មាន (inspect/read-only) ហើយកត់ត្រា baseline មុននឹងធ្វើពិសោធន៍។ កុំរត់ command ដែលប្ដូរ cgroup, firewall, kernel parameter, service, ឬ security policy លើម៉ាស៊ីនផលិតកម្ម។

## គោលដៅ

បន្ទាប់ពីរៀនចប់ អ្នកគួរអាចពន្យល់បានថា process ស្នើសេវា kernel ដូចម្តេច, container ប្រើ isolation/resource control ផ្នែកណា, systemd dependency ខុសគ្នាដូចម្តេច, និងចាប់ផ្តើម troubleshoot ពីភស្តុតាងជាក់ស្តែង។

## ឯកសារយោងផ្លូវការ

- [Linux namespaces manual](https://man7.org/linux/man-pages/man7/namespaces.7.html)
- [Linux capabilities manual](https://man7.org/linux/man-pages/man7/capabilities.7.html)
- [Linux seccomp manual](https://man7.org/linux/man-pages/man2/seccomp.2.html)
- [Kernel cgroup v2 documentation](https://docs.kernel.org/admin-guide/cgroup-v2.html)
- [systemd.unit documentation](https://www.freedesktop.org/software/systemd/man/latest/systemd.unit.html)
- [Linux kernel BPF documentation](https://docs.kernel.org/bpf/)
