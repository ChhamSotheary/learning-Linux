# មេរៀនទី ៣៖ Systemd — Dependencies និង Startup Order

## Unit និង Dependency

systemd គ្រប់គ្រង unit ដូចជា service, socket, mount និង target។ ក្នុង unit file ផ្នែក [Unit] អាចកំណត់ dependency។ ចំណុចសំខាន់៖ dependency ដែលទាញ unit មករត់ និង ordering ដែលកំណត់មុន/ក្រោយ គឺជារឿងខុសគ្នា។

- Wants= ទាញ unit ផ្សេងមកជាមួយដោយភាពទន់ជាង Requires=។
- Requires= កំណត់ requirement ខ្លាំងជាង ប៉ុន្តែមិនកំណត់ startup order ដោយខ្លួនឯងទេ។
- After= បញ្ជាក់លំដាប់ក្រោយ unit មួយ ប៉ុន្តែមិនទាញ unit នោះមករត់ដោយខ្លួនឯងទេ។
- Before= ជាលំដាប់ផ្ទុយនឹង After=។

ដូច្នេះការប្រើ Wants=network-online.target ជាមួយ After=network-online.target មានន័យផ្សេងពីការប្រើតែមួយ directive។ សេវាក៏ត្រូវមានរបៀបពិនិត្យ network availability ត្រឹមត្រូវតាម distro ផងដែរ។

## ពិនិត្យដោយមិនកែប្រែ

~~~bash
systemctl status ssh
systemctl cat ssh
systemctl show ssh -p Wants -p Requires -p After -p Before
systemctl list-dependencies --all ssh
~~~

ឈ្មោះ service ខុសគ្នាតាម distro; ប្រសិនបើ ssh មិនមាន សាកស្វែងរក unit ដែលមាន៖

~~~bash
systemctl list-unit-files --type=service
~~~

ការអាន unit file ពី disk អាចមិនបង្ហាញ state ដូច manager ដែលកំពុងដំណើរការទេ បើ file ទើបត្រូវបានកែ តែមិនទាន់ reload។

## ស្វែងរកបញ្ហា startup

~~~bash
systemctl --failed
journalctl -b -u ssh --no-pager
systemd-analyze critical-chain
~~~

កុំរត់ enable/disable/restart ឬកែ unit ក្នុងមេរៀននេះ។ នៅលើប្រព័ន្ធផលិតកម្ម ការប្តូរ dependency អាចរារាំង boot ឬបិទសេវាសំខាន់។

## លំហាត់

1. ជ្រើស service មួយដែលអ្នកស្គាល់ ហើយកត់ត្រា Wants, Requires និង After។
2. ពន្យល់ពីឧទាហរណ៍ដែល unit មួយត្រូវបានទាញមករត់ តែគ្មានការធានាលំដាប់។
3. ប្រើ journal ដើម្បីរកបន្ទាត់ error/warning ចុងក្រោយរបស់ service នោះ។ លុបឈ្មោះ host ឬទិន្នន័យឯកជនចេញមុនចែករំលែក។

## ឯកសារយោង

[systemd.unit documentation](https://www.freedesktop.org/software/systemd/man/latest/systemd.unit.html)
