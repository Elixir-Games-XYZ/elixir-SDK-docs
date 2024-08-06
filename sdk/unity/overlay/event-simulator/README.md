# Event Simulator

In production environments, the overlay is injected into the game by the Elixir Launcher. However, this is difficult to replicate during development. This is why we have created the Event Simulator.

<figure><img src="../../../../.gitbook/assets/telegram-cloud-photo-size-4-5997100708882661081-x.jpg" alt=""><figcaption><p>You can simulate connectivity with the Overlay in the Unity Editor</p></figcaption></figure>

The simulator allows you to test your game's integration with the Elixir Overlay event buffer without leaving Unity Editor.

You can access it in the editor's toolbar by clicking on `Elixir -> Overlay Event Simulator`

<figure><img src="../../../../.gitbook/assets/telegram-cloud-photo-size-4-5997100708882661097-m.jpg" alt=""><figcaption></figcaption></figure>

The simulator will open and be in the "Stopped" state. If you wish to test your integration, run the game and click on `Simulate`.

<figure><img src="../../../../.gitbook/assets/telegram-cloud-photo-size-4-5997100708882661100-m.jpg" alt=""><figcaption></figcaption></figure>

If everything goes well, the status of the simulator will now change from "Stopped" to "Simulating".

<figure><img src="../../../../.gitbook/assets/telegram-cloud-photo-size-4-5997100708882661101-x.jpg" alt=""><figcaption></figcaption></figure>

You will now be able to use the event simulator to see incoming [events](sdk-events.md) and send events to the game impersonating the overlay.
