pipeline {
    agent any

    environment {
        url_api = "http://truc"
    }

    stages {
        stage("etape1") {
            steps {
                echo "ce que je veux"
                script {
                    def unNom = 2
                    echo "${unNom}"
                    if (unNom > 1) {
                        echo "c'est plus grand que 1"
                    } else {
                        echo "Je sais pas compter"
                    }
                }
            }
        }
        stage("operations") {
            steps {
                script {
                    for (def i = 0; i < 3; i++) {
                        echo "Première boucle : ${i}"
                    }
                    for (i in 1..3) {
                        echo "Deuxième boucle : ${i}"
                    }
                    def cpt = 0
                    while (cpt < 3) {
                        echo "Troisième boucle : ${cpt}"
                        cpt++
                    }
                    def items = ["pomme", "poire", "Didier"]
                    items.each { item ->
                        echo "${item}"
                    }
                }
            }
        }
        stage("url-api") {
            steps {
                echo "va sur ... : ${url_api}"
            }
        }
        stage("approbation") {
            steps {
                input message: "continuer?", ok: 'Oui'
            }
        }
        stage("parallel_test") {
            parallel {
                stage("trycatch") {
                    steps {
                        script {
                            try {
                                def response = httpRequest 'https://httpbin.org/get'
                                println response.content
                            } catch (Exception e) {
                                error "erreur : ${e.message}"
                            }
                        }
                    }
                }
                stage("en mm temps") {
                    steps {
                        echo "abcd"
                        sleep 5
                        echo "en mm temps terminé"
                    }
                }
                stage("aussi") {
                    steps {
                        script {
                            def calc = 14 + 62000
                            echo "resultat : ${calc}"
                        }
                    }
                }
            }
        }
    }
    post {
        success {
            echo "ce que je veux s'est bien passé !"
        }
        failure {
            echo "ce que je veux ne s'est pas bien passé :("
        }
        always {
            echo "s'execute toujours"
        }
    }
}
