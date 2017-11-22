properties ([[$class: 'ParametersDefinitionProperty', parameterDefinitions: [
  [$class: 'StringParameterDefinition', name: 'mbed_os_revision', defaultValue: '', description: 'Revision of mbed-os to build. Use format "pull/PR-NUMBER/head" to access mbed-os PR']
  ]]])

if (params.mbed_os_revision == '') {
  echo 'Use mbed OS revision from mbed-os.lib'
} else {
  echo "Use mbed OS revisiong ${params.mbed_os_revision}"
  if (params.mbed_os_revision.matches('pull/\\d+/head')) {
    echo "Revision is a Pull Request"
  }
}

// List of targets with supported RF shields to compile
def targets = [
  "UBLOX_EVK_ODIN_W2": ["builtin"],
  // "REALTEK_RTL8195AM": ["builtin"], // Disabled because of https://github.com/ARMmbed/mbed-os/issues/5545
  "K64F": ["WIFI_ESP8266"],
  "NUCLEO_F401RE": ["WIFI_IDW0XX1"],
  "NUCLEO_F429ZI": ["WIFI_ESP8266"]
  ]

// Map toolchains to compilers
def toolchains = [
  ARM: "armcc",
  GCC_ARM: "arm-none-eabi-gcc",
  IAR: "IAR-linux"
  ]

// Supported RF shields
def radioshields = [
  "builtin",
  "WIFI_IDW01M1",
  "WIFI_ESP8266"
  ]

def stepsForParallel = [:]

// Jenkins pipeline does not support map.each, we need to use oldschool for loop
for (int i = 0; i < targets.size(); i++) {
    for(int j = 0; j < toolchains.size(); j++) {
        for(int k = 0; k < radioshields.size(); k++) {
            def target = targets.keySet().asList().get(i)
            def allowed_shields = targets.get(target)
            def toolchain = toolchains.keySet().asList().get(j)
            def compilerLabel = toolchains.get(toolchain)
            def radioshield = radioshields.get(k)

            def stepName = "${target} ${toolchain} ${radioshield}"
            if(allowed_shields.contains(radioshield)) {
              stepsForParallel[stepName] = buildStep(target, compilerLabel, toolchain, radioshield)
            }
        }
    }
}

timestamps {
  parallel stepsForParallel
}

def buildStep(target, compilerLabel, toolchain, radioShield) {
  return {
    stage ("${target}_${compilerLabel}_${radioShield}") {
      node ("${compilerLabel}") {
        deleteDir()
        dir("mbed-os-example-wifi") {
          checkout scm
          def config_file = "mbed_app.json"

          if ("${radioShield}" != "internal") {
            // Replace default rf shield
            execute("sed -i 's/\"value\": \"internal\"/\"value\": \"${radioShield}\"/' ${config_file}")
          }

          // Set mbed-os to revision received as parameter
          execute ("mbed deploy --protocol ssh")
          if (params.mbed_os_revision != '') {
            dir ("mbed-os") {
              if (params.mbed_os_revision.matches('pull/\\d+/head')) {
                execute("git fetch origin ${params.mbed_os_revision}:PR")
                execute("git checkout PR")
              } else {
                execute ("git checkout ${params.mbed_os_revision}")
              }
            }
          }
          execute("mbed new .")
          execute ("mbed compile --build out/${target}_${toolchain}_${radioShield}/ -m ${target} -t ${toolchain} -c --app-config ${config_file}")
        }
        stash name: "${target}_${toolchain}_${radioShield}", includes: '**/mbed-os-example-wifi.bin'
        archive '**/mbed-os-example-wifi.bin'
        step([$class: 'WsCleanup'])
      }
    }
  }
}
