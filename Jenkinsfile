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

                                    choices: ['ONE', 'TWO'], 

                                    name: 'PARAMETER_01'

                                ),
                                choice(

                                    choices2: ['ONE', 'TWO'],

                                    name: 'PARAMETER_02'

                                ),

                                booleanParam(

                                    defaultValue: true, 

                                    description: '', 

                                    name: 'BOOLEAN'

                                ),

                                text(

                                    defaultValue: '''

                                    this is a multi-line 

                                    string parameter example

                                    ''', 

                                     name: 'MULTI-LINE-STRING'

                                ),

                                string(

                                    defaultValue: 'scriptcrunch', 

                                    name: 'STRING-PARAMETER', 

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
