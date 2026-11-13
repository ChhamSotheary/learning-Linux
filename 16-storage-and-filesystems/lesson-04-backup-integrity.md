# មេរៀនទី ៤៖ Backup, Restore និង Integrity

Backup ដែលមិនធ្លាប់សាក restore គឺមិនទាន់បានបញ្ជាក់ថាអាចស្ដារបាន។ គោលការណ៍ 3-2-1 ជាគន្លឹះរៀបចំច្បាប់ចម្លង ប៉ុន្តែត្រូវបន្ថែម encryption, retention, access control, monitoring និងការធ្វើ restore drill។

## Checksum សម្រាប់ឯកសារសាកល្បង

~~~bash
sha256sum sample.tar
sha256sum -c sample.tar.sha256
~~~

checksum បញ្ជាក់ថា file ដូចគ្នានឹង checksum ដែលបានកត់ត្រា; វាមិនបញ្ជាក់ថាប្រភព backup គួរឱ្យទុកចិត្តទេ។ កុំដាក់ checksum និង backup តែមួយកន្លែង ប្រសិនបើគោលបំណងគឺរក corruption ឬការកែប្រែ។

## Restore drill

សាក restore ទៅ directory/VM ដាច់ដោយឡែក, ពិនិត្យ ownership/permission, បើក file សំខាន់, និងវាស់ពេលវេលា។ កុំ overwrite production ជាមួយ restore test។

## លំហាត់

សរសេរ runbook ស្ដារ service មួយ៖ អ្វីត្រូវ backup, encryption/key dependency, restore order, integrity check, owner ដែលអនុម័ត និង rollback plan។
