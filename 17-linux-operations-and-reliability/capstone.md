# Capstone៖ Linux Service Production Readiness

## គោលដៅ

រៀបចំ service សាកល្បងក្នុង VM ឱ្យអាចត្រួតពិនិត្យ, កំណត់សិទ្ធិ, backup និង troubleshoot បាន។ ប្រើតែ app/demo data មិនមែនទិន្នន័យពិត។

## Deliverables

- គំនូស architecture: process, systemd unit, network sockets, storage និង cgroup។
- Security review: user, capabilities, seccomp/LSM context, open ports, secrets និង image/service supply chain។
- Observability: health check, logs, CPU/memory/storage/network baseline និង alert/runbook។
- Recovery: backup, checksum/integrity និង restore drill ទៅ VM ដាច់ដោយឡែក។
- Incident report: timeline សម្រាប់ failure ដែលអ្នកបង្កើតក្នុង lab ដោយសុវត្ថិភាព (ឧ. បិទ demo service)។
- Change record: រាយការប្តូរ, success signal និង rollback។

## Rubric សម្រាប់វាយតម្លៃខ្លួនឯង

- អាចបង្ហាញភស្តុតាងសម្រាប់រាល់សេចក្តីសន្និដ្ឋាន។
- មិនដាក់ secret ឬទិន្នន័យរសើបក្នុង repo/log សាធារណៈ។
- អាចស្ដារ service ក្នុង lab និងបញ្ជាក់ថាទិន្នន័យត្រឹមត្រូវ។
- មាន runbook ដែលមនុស្សផ្សេងអាចអនុវត្តតាមបាន។
- បែងចែករវាងអ្វីដែលបានវាស់ និងអ្វីដែលនៅជាសម្មតិកម្ម។
