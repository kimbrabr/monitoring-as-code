# Monitoring-as-Code

📡 Развёртывание мониторинга инфраструктуры за 1 команду: Terraform + Ansible поднимают Prometheus, Loki, Grafana за ~2 минуты.

## 📌 Цель

Автоматизировать развёртывание мониторинга (Prometheus, Grafana, Loki) инфраструктуры или кластера с нуля, используя подход Infrastructure as Code.

## ⚙️ Стек технологий

- Terraform (сетевой стек / кластер / VM / k3s)
- Ansible (установка сервисов)
- Prometheus (метрики)
- Loki (логи)
- Grafana (дашборды)

## 🧱 Архитектура


## ✅ Acceptance-критерии

- [x] `terraform apply -auto-approve` отрабатывает без ошибок
- [x] `ansible-playbook site.yml -i inventory` ставит все сервисы
- [x] Prometheus: retention 3d, scrape interval 15s (`/config`)
- [x] Grafana:
  - Дашборд `node-exporter` (ID: 1860)
  - Кастомный дашборд `IoT`
- [x] Весь запуск (`apply → дашборд`) укладывается в < 2 мин

## 🔍 Проверки

- Все targets UP: `http://<pi>:9090/targets`
- Grafana: `http://<pi>:3000/d/node-exporter`
- Loki работает: `http://<pi>:3100/ready`
- Удаление без ошибок: `terraform destroy`

## 🚀 Быстрый старт

```bash
cd terraform/monitoring
terraform init
terraform apply -auto-approve

cd ../../ansible
ansible-playbook site.yml -i inventory
