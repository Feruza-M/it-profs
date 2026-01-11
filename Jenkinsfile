pipeline {
    agent any

    /* ===== ПАРАМЕТРЫ ===== */
    parameters {
        string(
            name: 'APP_VERSION',
            defaultValue: 'latest',
            description: 'Версия docker-образа'
        )

        choice(
            name: 'TARGET',
            choices: ['s3', 'docker-server', 'bare-metal'],
            description: 'Куда деплоить'
        )

        string(
            name: 'BRANCH',
            defaultValue: 'main',
            description: 'Ветка репозитория'
        )
    }

    stages {

        /* ===== 1. КЛОНИРОВАНИЕ ===== */
        stage('Checkout') {
            steps {
                echo "Клонируем репозиторий"
                git branch: params.BRANCH,
                    url: 'https://github.com/Feruza-M/it-profs.git'
            }
        }

        /* ===== 2. ПРОВЕРКА DOCKERFILE ===== */
        stage('Lint Dockerfile') {
            steps {
                echo "Проверяем Dockerfile"

                sh '''
                if ! command -v hadolint >/dev/null 2>&1; then
                    wget -qO hadolint https://github.com/hadolint/hadolint/releases/latest/download/hadolint-Linux-x86_64
                    chmod +x hadolint
                    mv hadolint /usr/local/bin/hadolint
                fi

                hadolint Dockerfile
                '''
            }
        }

        /* ===== 3. СБОРКА ===== */
        stage('Build image') {
            steps {
                echo "Собираем Docker image"

                sh "docker build -t it-profs:${params.APP_VERSION} ."
            }
        }
    }

    post {
        success {
            echo "Готово ✅"
        }
        failure {
            echo "Ошибка ❌"
        }
    }
}
