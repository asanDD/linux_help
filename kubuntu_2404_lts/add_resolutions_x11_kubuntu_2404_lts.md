 
Add resolutions on X11 on Kubuntu 24.04 LTS
=====================================

**Description:**<br>
Add additional resolutions to your display to chose from. Useful for gaming for example.

**Workaround:**<br>
\# Find screen names and existing resolutions<br>
`xrandr`<br><br>
\# Edit $HOME/.profile<br>
`sudo nano $HOME/.profile`<br><br>
\# Add the following function and edit the resolutions array 'resolutions' and the screens array 'screens' to your needs.

```
# dependencies: xrandr, cvt
add_resolutions() {
    # 16:9 resolutions
    # divisible by 8
    # 1280 x 720 | 1360 x 768 | 1408 x 792 | 1536 x 864 | 1664 x 936 | 1792 x 1008 | 1920 x 1080
    # not divisible by 8
    # 1360 x 765 | 1440 x 810 | 1600 x 900
    local -ar resolutions=(
        # width height frequency
        1360 768 60
        1408 792 60
        1536 864 60
        1664 936 60
        1792 1008 60
        1440 810 60
        1600 900 60
        )
    local -ar screens=( "HDMI-1" "eDP-1" )
    local screen=""
    local -a new_mode_array
    local new_mode_name=""
    local -ir len=${#resolutions[@]}
    local -i i=0
    local -i len_mode_array=0
    local -i index_modeline_default=12
    local -i index_modeline=0
    for ((i = 0 ; i < len ; i+=3)); do
        new_mode_array=( $( cvt ${resolutions[$i]} ${resolutions[((i+1))]} ${resolutions[((i+2))]} ) )
        len_mode_array=${#new_mode_array[@]}
        if [[ "${new_mode_array[$index_modeline_default]}" == "Modeline" ]]; then
            index_modeline=$((index_modeline_default + 1))
        else
            for ((index_modeline = 0 ; index_modeline < len_mode_array ; index_modeline++)); do
                if [[ "${new_mode_array[$index_modeline]}" == "Modeline" ]]; then
                    index_modeline=$((index_modeline + 1))
                    break;
                fi
            done
        fi
        if [[ "$index_modeline" < "$len_mode_array" ]]; then
            new_mode_name=$( tr -d \" <<< "${new_mode_array[$index_modeline]}" )
            index_modeline=$((index_modeline + 1))
            # echo "$new_mode_name"
            # echo "$new_mode_name ${new_mode_array[*]:$index_modeline}"
            xrandr --newmode "$new_mode_name" ${new_mode_array[@]:$index_modeline}
            for screen in "${screens[@]}"; do
                # echo "screen: $screen res: ${resolutions[$i]} ${resolutions[((i+1))]} ${resolutions[((i+2))]}"
                xrandr --addmode "$screen" "$new_mode_name"
            done
        fi

    done
}
add_resolutions  # exec the function
```



