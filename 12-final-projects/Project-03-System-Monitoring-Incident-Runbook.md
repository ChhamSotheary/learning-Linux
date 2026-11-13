# Final Project 03: System Monitoring និង Incident Runbook

## គោលដៅ

បង្កើត monitoring checklist និង runbook សម្រាប់សេវាកម្មមួយដែលអ្នកមានសិទ្ធិគ្រប់គ្រង។ ផ្តោតលើការប្រមូល evidence, ការប្រាស្រ័យទាក់ទង incident និងការធ្វើ recovery ដោយមានការអនុម័ត។

## តម្រូវការ

- កំណត់ service, owner, users និង expected behavior។
- ជ្រើស health indicators ដូចជា service state, disk, memory, CPU/load, network socket និង log errors។
- បង្កើត command checklist ដែលអាចរត់ read-only។
- កំណត់ threshold ដោយយោងទៅ baseline/workload មិនប្រើលេខស្មានជាស្តង់ដារទូទៅ។
- សរសេរ incident notes template និង escalation path។
- កំណត់ backup, recovery និង rollback procedures។
- សាកល្បង scenario ក្នុង VM/lab ដោយមិនប៉ះ production។

## Incident Scenario

បង្កើត lab simulation មួយ៖ service មិនឆ្លើយតប ឬ disk usage កើនឡើង។ ប្រមូល status, logs និង resource metrics មុនសម្រេចចិត្ត។ បែងចែក facts ពី hypothesis។ សរសេរ action ដែលត្រូវការអនុម័ត និងវិធី verify result។ កុំលុប logs ឬបិទ firewall ដើម្បីធ្វើឱ្យ alert បាត់។

## Deliverables

- Monitoring checklist និង baseline។
- Runbook មាន diagnostic steps, escalation និង rollback។
- Sample incident report ដែលលាក់ secrets/identifiers។
- Evidence ពី lab simulation និង lessons learned។
- Recovery/backup verification plan។

## Rubric

- Indicators ពាក់ព័ន្ធនឹង service: 20%
- Evidence-based troubleshooting: 25%
- Security/privacy ក្នុង logs: 15%
- Recovery និង rollback: 20%
- Runbook clarity និង escalation: 20%

## Self-review

- តើអ្នកថ្មីអាចអនុវត្ត runbook ដោយមិនសួរអ្នកនិពន្ធទេ?
- តើ diagnostic commands read-only មុន change?
- តើ threshold មាន evidence និង context?
- តើ rollback និង owner ត្រូវបានកំណត់?
- តើ sample logs បានលាក់ព័ត៌មានរសើប?
