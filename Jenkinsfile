pipeline {
    agent any
    stages {

        stage("Build")
        {
            steps
            {
                script {
                        echo "INFO: Build Stage"
                        sleep 60
                        properties([

                            parameters([

                                choice(

                                    choices: ['ONE', 'TWO', 'TREE'], 

                                    name: 'PARAMETER_02'

                                ),

                                booleanParam(

                                    defaultValue: true, 

                                    description: '', 

                                    name: 'BOOLEAN2'

                                ),

                                string(

                                    defaultValue: 'scriptcrunch', 

                                    name: 'STRING-PARAMETER2', 

                                    trim: true

                                )

                            ])

                        ])
                    }
            }
        }

        stage("Deploy")
        {
            steps
            {
                script {
                            echo "INFO: Deploy Stage"
                    }
            }
        }
    }
}
