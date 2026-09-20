# AI Skybox Cubemap Generator

An ai prompt for creating cubemap skyboxes

## The Prompt

Enter the below prompt into the ai of choice and be sure to customise it for specific output.

> Chat GPT 5.6 and above works quite well.

```
Create a Unity-compatible cubemap skybox from a scene description.

Do not generate the cubemap faces directly.

Follow this exact process:

First generate a true 2:1 equirectangular 360° panorama of the requested environment.

The panorama must be continuous around the full 360° horizon, cover the complete spherical field of view, and be suitable for spherical projection.

The left and right edges of the equirectangular panorama represent the same direction and must join continuously.

The panorama must contain valid environment imagery across the entire sphere, including directly overhead and directly below the viewer. Do not create black, transparent or empty regions.

Do not generate a cubemap, cubemap cross, individual cube faces, presentation sheet, labels, borders or annotations during this initial generation stage.

Generate only the clean 2:1 equirectangular panorama first.

SKYBOX LIGHTING REQUIREMENTS:

This environment will be used as a visual skybox inside Unity. The Unity scene will provide its own dynamic directional light and lighting system.

Do not bake a directional celestial light source into the skybox.

There must be no visible sun and no visible moon.

Do not include a solar disc, moon disc, concentrated sunset/sunrise glow, strong directional sunlight, god rays, sunbeams or other obvious celestial light source.

The sky should use relatively diffuse, direction-neutral atmospheric illumination so that the direction of the primary light can be controlled independently inside Unity.

Atmospheric colour variation is allowed, but it should not imply an obvious fixed position for the sun or moon.

Artificial light sources that belong to the environment, such as building lights, neon signs, digital displays and illuminated windows, are allowed.

SKYBOX DISTANCE REQUIREMENTS:

This environment will behave as an infinitely distant Unity skybox.

Avoid objects extremely close to the virtual camera.

Do not surround the camera with nearby walls, railings, pipes, rooftop equipment or other foreground objects.

Avoid large foreground surfaces that dominate the lower hemisphere.

The environment should have sufficient apparent distance from the camera to remain convincing when used as an infinitely distant background.

CONVERSION:

After the clean 2:1 equirectangular panorama has been generated, mathematically convert that panorama into six 1024×1024 cubemap faces.

Do not regenerate, repaint or independently approximate the cubemap faces.

Every cubemap face must be derived from the same equirectangular source using proper spherical-to-cube projection mathematics.

Use Unity's cubemap orientation:

    +Y


-X +Z +X -Z
-Y

Where:

Left = -X
Forward = +Z
Right = +X
Back = -Z
Up = +Y
Down = -Y

Then assemble the six projected faces into a 4096×3072 cubemap cross in exactly this layout:

    +Y


-X +Z +X -Z
-Y

EDGE VERIFICATION:

Verify all 12 shared cube edges.

This must include the correctly rotated/reversed edge relationships involving the +Y and -Y faces.

Matching pixels along every shared cube edge must have an RGB difference of exactly 0.

If the edge verification fails, correct the cubemap projection or edge orientation before exporting the final files.

EXPORT:

Export:

• one 4096×3072 cubemap cross PNG
• six individual 1024×1024 cubemap face PNGs (delete if not required)

Do not present the equirectangular panorama as the final deliverable.

The final deliverable must be the mathematically converted Unity cubemap.

SCENE DESCRIPTION:

<DESCRIBE THE SCENE IN DETAIL>

>> Example Scene Description
>> Create a vast cyberpunk-style city at dusk.
>> 
>> The city should contain dense futuristic skyscrapers, neon lighting, illuminated windows, elevated roads, bridges and large digital advertising boards.
>> 
>> Use neon colours including cyan, blue, magenta, pink, purple and red.
>> 
>> The city should feel enormous and extend for many kilometres in every horizontal direction.
>> 
>> Use multiple layers of buildings and strong atmospheric perspective, with increasingly distant structures gradually disappearing into thick urban haze and smog.
>> 
>> The sky should be heavily smog-filled and atmospheric, using dark blue, purple, magenta and subtle warm dusk tones.
>> 
>> The dusk illumination should remain diffuse and atmospheric. There must be no visible sun, moon or identifiable celestial light direction because the primary directional lighting will be provided dynamically inside Unity.
>> 
>> Large digital advertising boards should be distributed naturally throughout the architecture.
>> 
>> There should be no visible people or pedestrians.
>> 
>> The city should be in the far distance

CAMERA VERTICAL POSITION:

<DESCRIBE THE VERTICAL POSITION OF THE CAMERA IN THE SCENE>

>> Example Camera Position Description
>> Position the virtual camera approximately 20–30 metres above street level.
>> 
>> The camera should be low within the city rather than above the skyline.
>> 
>> The viewer should feel surrounded by the city, with most major skyscrapers extending substantially above the camera position.
>> 
>> The horizon should intersect the surrounding buildings rather than sitting above their rooftops.
>> 
>> Tall buildings should rise above the viewer in multiple directions.
>> 
>> Do not use an aerial, bird's-eye, high-altitude or skyline-overlook viewpoint.
>> 
>> At the same time, maintain enough distance between the camera and the nearest architecture for the environment to work naturally as an infinitely distant skybox.
>> 
>> The overall result should feel like the viewer is positioned within the city rather than looking down over it.
```

## The Viewer

`viewer/index.html` is a simple viewer page that will view the skybox cubemap textures.

Add a cubemap png to `viewer/textures/` directory and update the `viewer/textures/textures.json` file with the filename to make it available in the viewer dropdown.

Run `viewer/index.html` with a local http server.

```
cd viewer

# in python
python3 -m http.server 8000

# in php
php -S localhost:8000

# in ruby
ruby -run -e httpd . -p 8000

# in nodejs
npx http-server -p 8000
```

### Online Example

[https://labs.iceserve.co.uk/viewer/](https://labs.iceserve.co.uk/viewer/)
