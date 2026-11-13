# មេរៀនទី ៨៖ Security Boundary និង Threat Model របស់ Kernel

Kernel បែងចែក privilege រវាង user-space processes និងប្រព័ន្ធ។ ប៉ុន្តែ boundary មិនមានតែមួយទេ៖ UID/GID, capabilities, namespaces, seccomp, LSM, filesystem permissions និង cgroups មានតួនាទីខុសៗគ្នា។ កំហុសក្នុង configuration ឬ kernel/runtime អាចប៉ះពាល់ទៅ boundary ច្រើនជាន់។

## សំណួរ threat model

- អ្នកវាយប្រហារអាចគ្រប់គ្រង process មួយ ឬ user មួយ?
- Process អាចឃើញ filesystem, device, socket ឬ secret អ្វីខ្លះ?
- វាមាន capability អ្វី ហើយអាចហៅ syscall អ្វី?
- តើ LSM policy enforce ទេ? តើមាន audit logs?
- Resource limit ការពារប្រព័ន្ធពី exhaustion ដែរឬទេ?
- តើមាន update path និង rollback សម្រាប់ kernel/runtime?

## Inspect ដោយអាន

~~~bash
grep -E '^(Uid|Gid|CapEff|CapBnd|NoNewPrivs|Seccomp):' /proc/self/status
ls -l /proc/self/ns
~~~

ការមើល status មួយ process មិនបញ្ជាក់ថាប្រព័ន្ធទាំងមូល secure ទេ។ កុំបិទ SELinux/AppArmor, seccomp ឬ Secure Boot ក្នុងនាមជាការសាកល្បង។

## លំហាត់

សរសេរ threat model ១ ទំព័រសម្រាប់ demo service របស់អ្នក៖ asset, attacker, access path, boundary, detection និង recovery។ បែងចែក fact ដែលអ្នកបាន inspect ពី assumption។
