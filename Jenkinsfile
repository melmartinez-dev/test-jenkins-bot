pipeline {
    agent any
    environment {
        TOKEN = '2048197171:AAFaeFZUS_1PuL5vPKnTtTcstOJCDdTDLRo'
        CHAT_ID = '-1001403425116'
    }
    stages {
        stage('Hello') {
            steps {
                sendTelegram('<b>Test Message:</b> Building', env.TOKEN, env.CHAT_ID)
            }
        }
    }
    post {
        success {
            sendTelegram("<b>🔥 Deployment Successfull 🔥</b>\n\nSee job at <a href=\"${env.JOB_URL}\">${env.JOB_URL}</a>", env.TOKEN, env.CHAT_ID) 
        }
        failure {
            sendTelegram("<b>🚫 Deployment failed 🚫</b>\n\nSee job at <a href=\"${env.JOB_URL}\">${env.JOB_URL}</a>", env.TOKEN, env.CHAT_ID)
        }
    }
}

void sendTelegram(message, botToken, chatId) {
    def encodedMessage = URLEncoder.encode(message, "UTF-8")
    response = httpRequest (consoleLogResponseBody: false,
            contentType: 'APPLICATION_JSON',
            httpMode: 'GET',
            url: "https://api.telegram.org/bot${botToken}/sendMessage?text=${encodedMessage}&chat_id=${chatId}&disable_web_page_preview=true&parse_mode=HTML",
            validResponseCodes: '200')
}
