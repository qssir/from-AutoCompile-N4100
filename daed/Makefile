      - name: Inject Dynamic Hashes into Makefile
        run: |
          find . -type f -name "Makefile" -exec dos2unix {} \; -print || true
          
          # 安全更新变量：先删除旧定义，再在 PKG_NAME 后插入新值
          update_var() {
            local var="$1"
            local val="$2"
            local file="./daed/Makefile"
            sed -i "/^${var}:=/d" "$file"
            sed -i "/^${var} = /d" "$file"
            if grep -q "^PKG_NAME" "$file"; then
              sed -i "/^PKG_NAME/a ${var}:=${val}" "$file"
            else
              sed -i "1i ${var}:=${val}" "$file"
            fi
          }
          
          update_var "PKG_VERSION" "${{ needs.check_update.outputs.pkg_version }}"
          update_var "DAED_VERSION" "daed-${{ needs.check_update.outputs.latest_daed_short }}"
          update_var "WING_VERSION" "wing-${{ needs.check_update.outputs.latest_wing_short }}"
          update_var "CORE_VERSION" "core-${{ needs.check_update.outputs.latest_core_short }}"
          update_var "PKG_SOURCE_VERSION" "${{ needs.check_update.outputs.latest_daed_full }}"
          
          # 关键：删除旧的 PKG_HASH / PKG_MIRROR_HASH，避免 tarball 校验失败
          sed -i '/^PKG_HASH/d' ./daed/Makefile
          sed -i '/^PKG_MIRROR_HASH/d' ./daed/Makefile
          
          echo "=== Updated daed/Makefile ==="
          cat ./daed/Makefile
