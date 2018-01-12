- <span data-ttu-id="dd365-101">**パッケージ マネージャー UI** (Visual Studio): ソリューション エクスプローラーのソリューションを右クリックして、**[NuGet パッケージの復元]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="dd365-101">**Package Manager UI** (Visual Studio): right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="dd365-102">1 つまたは複数の個別のパッケージが、まだ適切にインストールされない場合 (ソリューション エクスプローラーにエラー アイコンが表示される)、パッケージ マネージャー UI を使用し、影響を受けるパッケージをアンインストールして再インストールします。</span><span class="sxs-lookup"><span data-stu-id="dd365-102">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall the affected packages and reinstall them.</span></span> <span data-ttu-id="dd365-103">「[パッケージの再インストールと更新](../Consume-Packages/Reinstalling-and-Updating-Packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dd365-103">See [Reinstalling and updating packages](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span></span>

- <span data-ttu-id="dd365-104">**コマンド ライン**: [nuget restore](../tools/cli-ref-restore.md) コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="dd365-104">**Command line**: use the [nuget restore](../tools/cli-ref-restore.md) command.</span></span> <span data-ttu-id="dd365-105">プロジェクト フォルダーで `nuget restore` を実行するだけで、プロジェクトの依存関係を復元しようとします。</span><span class="sxs-lookup"><span data-stu-id="dd365-105">Simply running `nuget restore` in the project folder attempts to restore the project's dependencies.</span></span>