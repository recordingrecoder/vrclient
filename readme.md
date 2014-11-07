## VRClient.js

Client library for HIRO VR browser.


## Basic usage


Include script into your project

    <script src="dom2thee.js"></script>


When your application is loaded and interactable, tell HIRO that we are ready to pull back the curtains by calling `ready()`

    VRClient.ready();


loading progress (WIP)

    VRClient.progress(1);   // 0 - 1 complete


When your application can safely be closed. (WIP)

    VRClient.ended();



## Callbacks

### Zero sensor

    VRClient.onZeroSensor = function() {
        // three.js VRControls for VR headset.
	    controls.zeroSensor();
	}


### Render mode changes

Handling different render mode changes


    // standard three.js webGL renderer
    var renderer = new THREE.WebGLRenderer();

    // render mode callback when HIRO render mode changes.
    VRClient.onRenderModeChange = function(mode) {
    	var modes = VRClient.renderModes;

    	if (mode == modes.mono) {
    	    // set effect to standard THREE.WebGLRenderer render
    		effect = renderer;

    		// mouse orbit controls
    		// http://threejs.org/examples/misc_controls_orbit.html
    		controls = new THREE.OrbitControls( camera );
    	} else if (mode == modes.stereo) {
    	    // Stereo effect renderer
    	    // http://threejs.org/examples/webgl_effects_stereo.html
    		effect = new THREE.StereoEffect( renderer );

    		// device accelerometer control
    	    // threejs.org/examples/misc_controls_deviceorientation.html
    		controls = new THREE.DeviceOrientationControls( camera );
    	} else if (mode == modes.vr) {
    		// VR headset orientation and position tracking
    		// threejs.org/examples/js/controls/VRControls.js
    		controls = new THREE.VRControls( camera );

    		// VR effect renderer
    		// threejs.org/examples/js/effects/VREffect.js
    		effect = new THREE.VREffect( renderer );
    	}

    	// resize handler
    }
