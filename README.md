# devops-netology

#Файлы, которые будут проигнорированы в будущем благодаря добавленному .gitignore:

#1) Локальные каталоги .terraform:
# **/.terraform/*

# 2) Файлы .tfstate: 
# *.tfstate
# *.tfstate.*

#2) Файлы журнала сбоев:
# crash.log
# crash.*.log

#3) Все файлы .tfvars, которые могут содержать конфиденциальные данные, такие как
#пароль, закрытые ключи и другие секреты.:
# *.tfvars
# *.tfvars.json

#4) Файлы переопределения, так как они обычноиспльзуются для локального переопределения ресурсов и т.д.
# override.tf
# override.tf.json
# *_override.tf
# *_override.tf.json

#5) Файлы конфигурации CLI:
# .terraformrc
# terraform.rc
#new line
