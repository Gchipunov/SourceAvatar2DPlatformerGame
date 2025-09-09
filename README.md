# SourceAvatar2DPlatformerGame
Make a mini game in vgui 
// In your custom panel's .cpp file

#include "inputsystem/iinputsystem.h"

// ... other includes

void CMyPlatformerPanel::OnThink()
{
    BaseClass::OnThink(); // Call the base class function

    // --- Your Game Logic Loop Starts Here ---

    // Example: Player Jump (KEY_SPACE)
    // We check the raw hardware state, ignoring VGUI focus completely.
    if ( g_pInputSystem->IsButtonDown( KEY_SPACE ) )
    {
        // To prevent jumping every single frame the key is held,
        // you need to manage the state yourself.
        if ( !m_bPlayerIsJumping )
        {
            PlayerJump(); // Your function to make the player jump
            m_bPlayerIsJumping = true;
        }
    }
    else
    {
        m_bPlayerIsJumping = false; // Reset when the key is released
    }

    // Example: Player Movement (KEY_A and KEY_D)
    float flPlayerSpeed = 5.0f;
    if ( g_pInputSystem->IsButtonDown( KEY_A ) )
    {
        m_vecPlayerPosition.x -= flPlayerSpeed;
    }

    if ( g_pInputSystem->IsButtonDown( KEY_D ) )
    {
        m_vecPlayerPosition.x += flPlayerSpeed;
    }

    // Update player physics, animation, etc.
    UpdatePlayer();
}
