# Projectiles Mod!

A mod for Icey.

This mod allows you to spam projectiles in Spring Cleaning 23 on Unity.

You need to be in a Photon room for the GUI to work.  
Press **TAB** to open and close the menu.

The GUI has almost all of the projectiles in the game.

---

## Script ∨

```csharp
using System.Collections;
using System.Collections.Generic;
using System.Reflection;
using UnityEngine;
using Photon.Pun;
using Photon.Realtime;
using UnityEngine.InputSystem;

public class projectiles : MonoBehaviour
{
    // script made by s1lly./ this script is for icey!
    // this script finds projectile hashes based of the prefab name, in the spring cleaning 23 update on gorilla tag

    PhotonView view;
    bool toggle1;
    bool toggle2;
    bool toggle3;
    bool toggle4;
    bool toggle5;
    bool toggle6;
    bool toggle7;

    // Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
    // IS THE POS OF WHERE THE PROJECTILES COME FROM
    // SO IF U WANT IT TO COME OUT THE HEAD DO:
    // Vector3 slingshotLaunchLocation = GorillaTagger.Instance.headCollider.transform.position;

    void SnowBalls()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("SnowballProjectile");
        int projtrail = -1;
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    void slingshotspam()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("SlingshotProjectile");
        int projtrail = FindTrailHash("SlingshotProjectileTrail");
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    void cloudslingshot()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("CloudSlingshot_Projectile");
        int projtrail = FindTrailHash("CloudSlingshot_ProjectileTrailFX");
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    void cupidarrow()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("CupidArrow_Projectile");
        int projtrail = FindTrailHash("CupidArrow_ProjectileTrailFX");
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    void elfbow()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("ElfBow_Projectile");
        int projtrail = FindTrailHash("ElfBow_ProjectileTrail");
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    void horns()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("HornsSlingshotProjectile_PrefabV");
        int projtrail = FindTrailHash("HornsSlingshotProjectileTrail_PrefabV");
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    void iceslingshot()
    {
        Vector3 slingshotLaunchLocation = GorillaTagger.Instance.rightHandTransform.position;
        Vector3 slingshotLaunchVelocity = new Vector3(10, 10, 10);
        int projHash = FindPoolHashByName("IceSlingshotProjectile_PrefabV Variant");
        int projtrail = FindTrailHash("IceSlingshotProjectileTrail Variant");
        bool forlefthand = false;
        int count = 30;

        view.RPC(
            "LaunchSlingshotProjectile",
            RpcTarget.All,
            slingshotLaunchLocation,
            slingshotLaunchVelocity,
            projHash,
            projtrail,
            forlefthand,
            count
        );
    }

    bool showMenu = false;
    Rect windowRect = new Rect(50, 50, 220, 260);

    Color normalColor = new Color(0.15f, 0.15f, 0.15f, 1f);
    Color redColor = Color.red;

    float fade = 0f;
    bool fadeUp = true;

    void Update()
    {
        if (view == null)
        {
            if (PhotonNetwork.InRoom && GorillaGameManager.instance != null)
            {
                view = GorillaGameManager.instance.photonView;
                Debug.Log("Projectile script: PhotonView assigned!");
            }
        }

        if (Keyboard.current.tabKey.wasPressedThisFrame)
            showMenu = !showMenu;

        if (fadeUp)
        {
            fade += Time.deltaTime * 1.5f;
            if (fade >= 1f)
            {
                fade = 1f;
                fadeUp = false;
            }
        }
        else
        {
            fade -= Time.deltaTime * 1.5f;
            if (fade <= 0f)
            {
                fade = 0f;
                fadeUp = true;
            }
        }
    }

    void OnGUI()
    {
        if (!showMenu) return;

        GUI.backgroundColor = Color.Lerp(normalColor, redColor, fade);
        windowRect = GUI.Window(0, windowRect, DrawMenu, "Projectiles test thing idk");
    }

    void DrawMenu(int id)
    {
        toggle1 = GUI.Toggle(new Rect(10, 30, 200, 20), toggle1, "Snow Balls");
        toggle2 = GUI.Toggle(new Rect(10, 55, 200, 20), toggle2, "Sling Shot");
        toggle3 = GUI.Toggle(new Rect(10, 80, 200, 20), toggle3, "CloudSlingShot");
        toggle4 = GUI.Toggle(new Rect(10, 105, 200, 20), toggle4, "Cupid Arrow");
        toggle5 = GUI.Toggle(new Rect(10, 130, 200, 20), toggle5, "Elf Bow");
        toggle6 = GUI.Toggle(new Rect(10, 155, 200, 20), toggle6, "Horns");
        toggle7 = GUI.Toggle(new Rect(10, 180, 200, 20), toggle7, "Ice SlingShot");

        if (toggle1) SnowBalls();
        if (toggle2) slingshotspam();
        if (toggle3) cloudslingshot();
        if (toggle4) cupidarrow();
        if (toggle5) elfbow();
        if (toggle6) horns();
        if (toggle7) iceslingshot();

        GUI.DragWindow(new Rect(0, 0, 10000, 20));
    }

    private int FindPoolHashByName(string prefabName)
    {
        foreach (KeyValuePair<int, SinglePool> keyValuePair in
            (ObjectPools.instance.GetType().GetField("lookUp", BindingFlags.Instance | BindingFlags.NonPublic)
            .GetValue(ObjectPools.instance) as Dictionary<int, SinglePool>))
        {
            if (keyValuePair.Value.objectToPool.name == prefabName)
                return keyValuePair.Key;
        }

        Debug.LogError("Pool with prefab name '" + prefabName + "' not found.");
        return -1;
    }

    private int FindTrailHash(string projectileName)
    {
        foreach (KeyValuePair<int, SinglePool> keyValuePair in
            (ObjectPools.instance.GetType().GetField("lookUp", BindingFlags.Instance | BindingFlags.NonPublic)
            .GetValue(ObjectPools.instance) as Dictionary<int, SinglePool>))
        {
            string name = keyValuePair.Value.objectToPool.name;

            if (name.Contains(projectileName) && name.Contains("Trail"))
                return keyValuePair.Key;
        }

        Debug.LogError("Trail for '" + projectileName + "' not found.");
        return -1;
    }
}
```
