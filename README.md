<a id="readme-top"></a>



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/github_username/repo_name">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">Opentrons OT-2 HTTP API Python wrapper</h3>

  <p align="center">
    This project aims to create a simple Python wrapper that would allow to use the Opentrons OT-2 liquid handling robot in a direct and reactive way, without the need to upload protocols onboard the robot's RPi.
    <br />
    
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project


This project is meant to help researchers and engineers who are in the process of creating a custom liquid handling system on top of the Opentrons OT-2 robot. If you find yourself in a situation where using the default protocol system for the OT-2 isn't working out of you, this project might be useful. 

**Example use case:** The OT-2 needs to be outfitted with an external camera and its movements need to be controlled based on the information observed with the camera. Since the protocols that use the stock OT-2 Python API from Opentrons need to be executed directly on the robot, non-built-in python modules can't be used (in this case, you might want to use the OpenCV module, but would be unable to do so). With this wrapper, you would be able to control the robot directly from your computer, using any packages you want in the process. 
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->
## Getting Started

Currently, the wrapper is not in package form. It is simple to use nonetheless. 

### Prerequisites

Potentially, any version of Python. All packages are base Python packages like `requests`, `json`, `functools`.

### Installation
While the project is not in package form, use `git clone`, change the IP address in the `BASE_URL` in the `OpentronsAPI` class in the `ot2_api.py` file. The wrapper should be ready to use after that. 
<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage
Start by initializing an object of the `OpentronsAPI` class:

    ot2_api = OpentronsAPI()

Continue to test the connection by toggling the led lights of the OT-2:

    ot2_api.toggle_lights()
Home the robot:

    ot2_api.home_robot()

In order to issue commands to the OT-2, a run needs to be created:

    ot2_api.create_run()
 Next, a pipette needs to be loaded. By default, the pipette is `"p300_single_gen2"`. If this needs to be changed to a multipipetter, change the `self.PIPETTE` variable in the class instance or locally. 
 
    ot2_api.load_pipette(mount='left')

If you are using a Jupyter notebook to control the robot, you might encounter a dead kernel from time to time. When the kernel dies, the variables of the loaded labware, pipette, etc. are lost. To reload the run with all the variables, you can use the following command. The response contains `json` dictionaries of all of the previous runs, as well as the current. To look at a run in detail, index through the response list.

    response = ot2_api.get_run_info()

Load labware command. After the labware is loaded, the unique ID of the labware is stored in the class instance `ot2_api.labware_dct` variable.

    #Define the api_name of the labware:
    TIP_RACK = "opentrons_96_tiprack_300ul"
    #Load the labware into deck slot "1":
    ot2_api.load_labware(TIP_RACK, 1)

Pick up tip "A1" from tip rack in slot "1":

    ot2_api.pick_up_tip(openapi.labware_dct['1'], 'A1')

Move to coordinates:

    ot2_api.move_to_coordinates((x,y,z), min_z_height=1)

Aspirate in place:

    ot2_api.aspirate_in_place(volume = 25, flow_rate = 25)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

- [ ] TBD

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Ivan Stepanov -  steiva@uw.edu

Project Link: https://github.com/steiva/opentrons-ot2-http-python-wrapper

<p align="right">(<a href="#readme-top">back to top</a>)</p>





